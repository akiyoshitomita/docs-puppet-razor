---
title: OSインストール動作の説明 
summary: ノードの基本シーケンス説明
authors:
  - A.Tomita 
date: 2019-05-28 
---

# 基本動作説明

ここでは、Puppet razorがノードの検出動作からOSのインストールが終わるまで基本的な動作を説明します。

大きく分けて、以下のステップで動作します。

1. ノードの検出及びノードの情報収集
1. OSのインストール
1. OSの起動


## ノードの検出及びノードの情報収集

1. ノードのPXE動作
    * ノードがDHCPリクエストをDHCPサーバへ送信  
    * DHCPサーバは、TFPTサーバのiPXEのイメージファイル(ipxe.efi)から
      起動するように指定してDHCPリプライを返す 
    * ノードから、TFTPサーバのiPXEイメージを取得して、iPXEイメージで起動

1. ノードのiPXE動作  
    * iPXEファームウェアから、DHCPオプション175を付けたDHCPリクエストをDHCPサーバへ送信  
    * DHCPサーバは、ipxe用の設定ファイル(bootstrap.ipxe)をブートイメージとして指定し
      DHCPリプライを返す  
    * iPXEファームウェアは、bootstrap.ipxeに記載されているrazorサーバのURLへHTTPアクセス
    * razorサーバから、razorマイクロカーネルのURLを送信
    * iPXEファームウェアは、razorマイクロカーネルをHTTPダウンロードして、razorマイクロカーネルを起動

1. ノードのrazorマイクロカーネル動作  
    * razorマイクロカーネルは、DHCPサーバからIPを取得  
    * razorマイクロカーネルは内部のfactsプログラムによりノードの状態を収集  
    * razorマイクロカーネルから、razorサーバへfactsの情報を送信  
    * razorサーバから、再起動支持を受け取り再起動  

!!! note "再起動について"
    インストールするOSがrazorサーバ上で決定していない場合は、再起動動作は起きません

## OSのインストール

1. ノードのPXE動作
    * ノードがDHCPリクエストをDHCPサーバへ送信  
    * DHCPサーバは、TFPTサーバのiPXEのイメージファイル(ipxe.efi)から
      起動するように指定してDHCPリプライを返す 
    * ノードから、TFTPサーバのiPXEイメージを取得して、iPXEイメージで起動

1. ノードのiPXE動作  
    * iPXEファームウェアから、DHCPオプション175を付けたDHCPリクエストをDHCPサーバへ送信  
    * DHCPサーバは、ipxe用の設定ファイル(bootstrap.ipxe)をブートイメージとして指定し
      DHCPリプライを返す  
    * iPXEファームウェアは、bootstrap.ipxeに記載されているrazorサーバのURLへHTTPアクセス
    * razorサーバから、OSのネットワークインストーラのURLを送信
    * iPXEファームウェアは、指定されたネットワークインストーラーを起動

1. ネットワークインストーラ動作
    * 各種OSのネットワークインストーラの動作に従って動作

!!! node "インストールオプションについて"
    RedHat/CentOS/fedoraの場合は、kick start  
    Ubuntu/Debianの場合は、preseed
    にてオプション指定ができます。

## OSの起動

1. ノードのPXE動作
    * ノードがDHCPリクエストをDHCPサーバへ送信  
    * DHCPサーバは、TFPTサーバのiPXEのイメージファイル(ipxe.efi)から
      起動するように指定してDHCPリプライを返す 
    * ノードから、TFTPサーバのiPXEイメージを取得して、iPXEイメージで起動

1. ノードのiPXE動作  
    * iPXEファームウェアから、DHCPオプション175を付けたDHCPリクエストをDHCPサーバへ送信  
    * DHCPサーバは、ipxe用の設定ファイル(bootstrap.ipxe)をブートイメージとして指定し
      DHCPリプライを返す  
    * iPXEファームウェアは、bootstrap.ipxeに記載されているrazorサーバのURLへHTTPアクセス
    * razorサーバから、プライマリHDDから起動するように指示
    * iPXEファームウェアは、プライマリHDDから起動

