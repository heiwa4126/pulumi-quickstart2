# pulumi-quickstart2

[Get Started with AWS | Pulumi](https://www.pulumi.com/docs/get-started/aws/)を見て作った
2番めののプロジェクト
(最初のプロジェクトはaws-goでやったらpulumi upにCPUが耐えられなかった)。


# 手順

```bash
export AWS_ACCESS_KEY_ID=<YOUR_ACCESS_KEY_ID>
export AWS_SECRET_ACCESS_KEY=<YOUR_SECRET_ACCESS_KEY>
mkdir quickstart && cd quickstart
pulumi new aws-python
# リージョンとか聞かれる。
# 特定のwwwページにアクセスするよう言われる。githubでログインした。
# venvを自動で作りpipも勝手にやる。
. ./venv/bin/activate
vim __main__.py  # S3バケット名だけ変える
pulumi up
```

あとは [Get Started with AWS | Pulumi](https://www.pulumi.com/docs/get-started/aws/)
に従って、S3バケットにWWWアクセスできるところまで。


# ほかメモ

gitにはvenvは入ってないのでクローン先では

```bash
git clone xxxxx
cd xxxx
python3 -m venv ./venv
. ./venv/bin/activate
# で、
pulumi stack select dev
# または
pulumi stack new dev2
pulumi config set aws:region us-east-2
# で
pulumi up  # pip install -r requirements.txtは自動でやってくれる(手動でもいいけど)
```

しないとダメだ。
このへんが「既存の言語が使える」の欠点。


# コマンド補完

参考: [Command\-line Completion](https://www.pulumi.com/docs/reference/cli/#command-line-completion)

```bash
pulumi gen-completion bash > ~/.pulumi/bash_completion
```
して

~/.profile (かそれに該当するあれ)に
```bash
# Pulumi completion
if [ -f "$HOME/.pulumi/bash_completion" ] ; then
   .  "$HOME/.pulumi/bash_completion"
fi
```


# 感想

- AWS CDKに似ているが、AWS CDKの1000倍早い。
- 既存言語で書けるのはCDK同様だが、YAMLでも書ける。
- Terraformのbackendにあたるのが Pulumiのweb一択。GitHubActionみたいなUIがついてる。
- チームで使うなら有料。
- ~/.aws/credentials とかは見てくれない。環境変数をexport
