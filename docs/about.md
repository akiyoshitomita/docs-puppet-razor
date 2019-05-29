---
title: puppet razorとは
summary: Puppet razorの説明文 
authors:
  - A.Tomita 
date: 2019-05-29 
---

# puppet razorとは

## 概要

Puppet社が開発したソフトウェアで、
PXEを利用したネットワーク環境にて、ネットワーク内のPXEクライアントの管理を行う仕組みです。

主にデータセンター内のベアメタルサーバのプロビジョニングに利用され、
任意のOSをインストールする時に利用します。

機能は、PXEクライアントの検出、OSのインストール、インストール後の初回スクリプト実行が
できます。

puppet社が開発したものですが、必ずしも自動化ツールのPuppetと組み合わせて利用する必要は
ありません。


## 利用に関して

Puppet razorは、Apache2.0 ライセンスで作られており、誰もが自由に利用することができます。


## サポートについて

OSSのソフトウェアのため、コミュニティサポートになります。  

メーカーサポート（有償）が欲しい方は、Puppet Enterpriseを購入すると
有償サポートが受けられますが、利用できる環境が限定されます。
有償版の詳しい内容は、Puppet Enterpriseマニュアル内の
[Provisioning with Razor](https://puppet.com/docs/pe/latest/provisioning_with_razor.html)
を参照してください。



