---
title: システムコンポーネントの説明
summary: コンポーネントリスト 
authors:
  - A.Tomita 
date: 2019-05-28 
---

# システムコンポーネント

## コンポーネント一覧 

Puppet Razorのコンポーネントを説明します。

### razor サーバ 

ネットワーク上存在するノード(PXEクライアント)の制御を行うための
管理サーバです。
各ノードと連携を行い、情報収集やOSのインストールを行います。

Java + JRubyで作れており、JavaとJRubyの実行環境が必要になります。
各ノードのデータは、PostgreSQLサーバに保存します。

* [razor サーバ GITHUB](https://github.com/puppetlabs/razor-server)

### razor クライアントツール 

シェル上でzazor サーバの操作を行うための管理コマンドツールです。
rubyで作られているため、rubyの実行環境が必要になります。

※　REST-APIを経由して、直接razorサーバとやり取りを行う場合はインストールする必要は
ありません。

* [razor クライアントトール GITHUB](https://github.com/puppetlabs/razor-client)


### PostgreSQLサーバ

データベースサーバであり、
razorサーバの情報を蓄積するために利用します。

* [PostgreSQL オフィシャルサイト](https://www.postgresql.org/)


### DHCPサーバ/TFTPサーバ/DNSサーバ

PXEの動作をするための、DHCPサーバとTFTPサーバです。  
1台で済ませる場合は、dnsmasqが利用されますが、他のプロダクトでも可能です。

DHCPサーバは、DHCPオプションを元に、任意のDHCPのBootオプションを切り替えれる機能が必要です。

TFTPサーバは、ファイルのRead権限があるものが必要です。
保存するファイルは、数十キロバイト程度のため、RFC2348に準拠する必要はありません。

DNSサーバは、razor サーバのホスト名を解決できるようにする必要があります。

* [dnsmasq オフィシャルサイト](http://www.thekelleys.org.uk/dnsmasq/doc.html)


### razor マイクロカーネル

CentOSベースで作成されたネットワークブート用のイメージです。
ノードが初めてPXEブートした時に、ネットワークを通じてノードのメモリ上に展開され
razorサーバに対してノードの情報を送信するために利用します。

* [razor マイクロカーネル GITHUB](https://github.com/puppetlabs/Razor-Microkernel)


### iPXE 

OSSで開発されている、クライアントファームウェア兼ブートローダです。
razorのシステムでは、ブートローダとして動作し、razorマイクロカーネルからの起動、
ネットワークからOSのインストール(各OSのインストーラーを利用)、ローカルディスクからの起動を
切り替えるのに利用されます。

* [iPXE オフィシャルサイト](http://ipxe.org/)

