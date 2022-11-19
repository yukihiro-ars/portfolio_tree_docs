# yamlを使った項目チェックについて

- [yamlを使った項目チェックについて](#yamlを使った項目チェックについて)
  - [基本ルール](#基本ルール)
  - [キャリアシート項目チェック定義](#キャリアシート項目チェック定義)
  - [プロフィール項目チェック定義](#プロフィール項目チェック定義)
  - [yaml解析について](#yaml解析について)

## 基本ルール

- validを直接内包するキー(career.biz_typeなど)は、value必須
- validを直接内包しないキー(career, career.techなど)は、value未設定

## キャリアシート項目チェック定義

~~~yaml

career:
    logic_name: 'キャリアシート'
    biz_type:
        logic_name: '業種'
        valid:
            - require
            - unique 
    overview:
        logic_name: 'プロジェクト概要'
        valid:
            - require
            - unique
    detail:
        logic_name: '担当業務詳細'
        valid:
            - require
            - unique
    term_start:
        logic_name: '期間開始'
        valid:
            - require
            - unique
            - format_YYYYMMDD 
    term_end:
        logic_name: '期間終了'
        valid:
            - unique 
            - format_YYYYMMDD
    role:
        logic_name: '役割'
        valid:
            - require
            - any
    phase:
        logic_name: '工程'
        valid:
            - require
            - any
    scale:
        logic_name: '規模'
        valid:
          - unique 
    tech:
        logic_name: '技術'
        infra:
            logic_name: 'インフラ'
            valid:
                - require
                - any
        middle:
            logic_name: 'ミドル'
            valid:
                - require
                - any
        strage:
            logic_name: 'ストレージ'
            valid:
                - require
                - any
        lang:
            logic_name: '言語'
            valid:
                - require
                - any
        other:
            logic_name: 'その他'
            valid:
                - any
~~~

## プロフィール項目チェック定義

~~~yaml

profile:
    logic_name: 'プロフィール'
    md:
        logic_name: 'md'
        valid:
            - require
            - unique 
            - blob
~~~

## yaml解析について

- FE
  - 解析不要
  - Yamlフォーマットごとに実装
- BE
  - snakeYamlを利用した解析を検討
  - 項目チェックはCMSクライアントとBEにて実施
    - CMSクライアント
      - 項目の親子関係チェック
      - keyの妥当性チェック
    - BE
      - 項目の親子関係チェック
      - keyの妥当性チェック
      - 参照可能ノードチェック(require項目が充足しているか)
