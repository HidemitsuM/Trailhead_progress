# 2023 Dec 12-13 Trailhead進捗🗻🏃💦

## 🏃💨進捗状況

### 開発者中級

- [x] Find and Fix Bugs wiht Apex Replay Debugger `2023/12/6 完了`
  - [x] Launch Your Trailhead Playground
  - [x] Set Up Visula Studio Code
  - [x] Set Up Apex Replay Debugger
  - [x] Debug Your Code
- [x] [Apexテスト](https://trailhead.salesforce.com/ja/content/learn/modules/apex_testing?trail_id=force_com_dev_intermediate) `2023/12/12 完了`
  - [x] [Apex単体テストを始める](https://trailhead.salesforce.com/ja/content/learn/modules/apex_testing/apex_testing_intro?trail_id=force_com_dev_intermediate)
  - [x] [Apexトリガをテストする](https://trailhead.salesforce.com/ja/content/learn/modules/apex_testing/apex_testing_triggers?trail_id=force_com_dev_intermediate)
  - [x] [Apexテストのテストデータを作成する](https://trailhead.salesforce.com/ja/content/learn/modules/apex_testing/apex_testing_data?trail_id=force_com_dev_intermediate)

## 🧻ToC

- [2023 Dec 12-13 Trailhead進捗🗻🏃💦](#2023-dec-12-13-trailhead進捗)
  - [🏃💨進捗状況](#進捗状況)
    - [開発者中級](#開発者中級)
  - [🧻ToC](#toc)
  - [🐞Find and Fix Bugs wiht Apex Replay Debugger `2023/12/06 完了`](#find-and-fix-bugs-wiht-apex-replay-debugger-20231206-完了)
    - [🐞Launch Your Trailhead Playground](#launch-your-trailhead-playground)
    - [🐞Set Up Visula Studio Code](#set-up-visula-studio-code)
    - [🐞Set Up Apex Replay Debugger](#set-up-apex-replay-debugger)
    - [🐞Debug Your Code](#debug-your-code)
  - [🔍Apexテスト `2023/12/12 完了`](#apexテスト-20231212-完了)
    - [🔍Apex単体テストを始める](#apex単体テストを始める)
    - [🔍Apexトリガをテストする](#apexトリガをテストする)
    - [🔍Apexテストのテストデータを作成する](#apexテストのテストデータを作成する)
  - [🧠復習の必要性について](#復習の必要性について)

## 🐞Find and Fix Bugs wiht Apex Replay Debugger `2023/12/06 完了`

### 🐞Launch Your Trailhead Playground

### 🐞Set Up Visula Studio Code

- **一応テスト自体はコード上の`Run Test`をクリックすることでできてはいるが，Trailhead⛰に書いてある`> SFDX: Run Apex Tests`での実行に非常に時間がかかる...**
  - 原因不明

- `Methods defined as TestMethod do not support Web service callouts`のエラーメッセージが出ている状態.
  - `Mock`を追加することで`callout`によるエラーを回避可能みたいな情報はあるものの，そもそも`callout`してなくないかという話
  - ~~また，Trailheadのチュートリアルにあるように修正しても依然としてテストが`Fail`なので原因の解決には至らず...環境構築の問題???~~

--> Salesforce CLI integrationといい，各種トラブルに再現性がないのは環境構築をミスっている可能性...

```markdown
JDK バージョン 17 (推奨)、JDK バージョン 11、または JDK バージョン 8 のいずれかのインストールが必要です
```

### 🐞Set Up Apex Replay Debugger

- **Run Apex Testsの開始が非常に遅い.実行自体は可能．(だけどめっちゃ遅い)**
- ~~calloutしていないはずなのにcalloutによるエラーが発生しており，これを解決できない．~~

### 🐞Debug Your Code

結局`Playground`を新規でつくったら何事もなく通ってしまった...
**メモ供養👏南無**

## 🔍Apexテスト `2023/12/12 完了`

### 🔍Apex単体テストを始める

コードのカバー率についての理解が若干不足...
てっきり各分岐のチェックをすべて網羅してカバー率100%になるのかと思いきや，ハンズオンにおいては2パターンの検証のみで完結してしまった．

### 🔍Apexトリガをテストする

```java
@isTest
public class TestRestrictContactByName {
    
    @isTest static void test1(){
        
        //姓が`INVALIDNAME`な状態のContactを追加・更新可能かどうか
        Contact con = new Contact(LastName = 'INVALIDNAME');

        try{
            //insertに挑戦
            insert con;
            
        } catch(Exception e){
            //エラーを取得して想定通りかどうかを確認
            System.assertEquals(e.getMessage(), 'The Last Name "INVALIDNAME" is not allowed for DML');
        }
    }
}
```

エラーのケース以外に正常終了のケースのテスト方法について...

### 🔍Apexテストのテストデータを作成する

```java
//最初に作成したクラス
public class RandomContactFactory {
    
    public static list<Contact> generateRandomContacts (Integer int_cnumber, String str_clastname){
        List<Contact> contact_list = new List<Contact>();
        
        // codeblock
        for(integer i = 0; int_cnumber < i; i++){
            Contact c = new Contact(FirstName = 'testContact', LastName = str_clastname);
            contact_list.add(c);
        }
        
        return contact_list;
        
    }
        
}

// 「generateRandomContacts」メソッドの実行が失敗しました。メソッドが存在しないか、静的ではないか、取引先責任者レコードの正しいセットを返しませんでした。
// for loop 内の `int_number < i`が誤り．正しくは `i < int_number`であった．
```

## 🧠復習の必要性について

- 開発者初級/中級に出てきた内容は必ずできるようにしたい．
  - コードを記述するケースにおいて，記述する内容自体はキメラでもいいが，動作や動きに対する理解は必要ですよ，と(まぁ当たり前...)
- 各セクションで取り組んだ内容を自分なりに多少変化させて定着を図る．
  - 「ここの動作は？」って聞かれた際に脊髄反射⚡で解答できるようにする．
    - 経験値なくしてコーディングの成長はないって話
    - Playgroundをいじり倒す🤏🤏🤏
