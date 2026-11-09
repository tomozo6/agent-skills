# agent-skills

Codexなどのエージェントで使うスキル集です。スキルごとに、実行手順と必要な補助ファイルをまとめています。

## スキル一覧

| スキル | 用途 |
|---|---|
| [cve-assessment](skills/cve-assessment/README.md) | コンテナの構成情報と公式告知から、指定されたCVEの対応要否を判定する |

## 導入

### npxで導入する

GitHubに公開されたスキルを、Vercel製の[skills CLI](https://github.com/vercel-labs/skills)で導入できます。Node.js 22.20以上とnpm（npx）が必要です。このリポジトリをnpmへ公開する必要はありません。

Codexで全プロジェクトから利用する場合は、`-g`を付けます。

```bash
npx skills add tomozo6/agent-skills --skill cve-assessment -a codex -g
```

特定のプロジェクトだけで利用する場合は、導入先のプロジェクトで`-g`を外して実行します。

```bash
npx skills add tomozo6/agent-skills --skill cve-assessment -a codex
```

複数のスキルや対応エージェントから対話形式で選ぶ場合は、次のコマンドを実行します。

```bash
npx skills add tomozo6/agent-skills
```

`--skill`は導入するスキル名、`-a codex`は利用するエージェントの指定です。各スキルの実行に必要な環境は、スキルごとのREADMEを参照してください。

### 手動で導入する

必要なスキルのフォルダ全体を、利用するエージェントのスキル配置先へコピーします。`SKILL.md`に加え、`scripts/`・`references/`などの付属ファイルも必要です。

Codexでプロジェクト単位に導入する例です。導入先のプロジェクトで実行します。

```bash
git clone https://github.com/tomozo6/agent-skills.git /tmp/tomozo6-agent-skills
mkdir -p .agents/skills
cp -R /tmp/tomozo6-agent-skills/skills/cve-assessment .agents/skills/
```

同名のスキルがすでにある場合は、ローカルでの変更を確認してから更新してください。導入後は新しいチャットでスキル名を指定して利用できます。利用例・前提条件は各スキルのREADMEを参照してください。

## 構成

```text
skills/
└── cve-assessment/
    ├── SKILL.md          # エージェント向けの手順
    ├── README.md         # 利用者向けの説明
    ├── agents/           # 表示・呼び出し用メタデータ
    ├── scripts/          # 補助処理とテスト
    └── references/       # 入出力仕様・調査上の注意
```

各スキルは、そのフォルダ内のファイルで利用できる構成にします。実際の構成情報・調査結果・キャッシュは公開用ファイルに含めません。
