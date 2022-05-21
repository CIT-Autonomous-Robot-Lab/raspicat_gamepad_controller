# raspicat_gamepad_controller

Raspberry Pi Catを家庭用ゲームコントローラ (Logicool Wireless Gamepad F710) を用いて操作するためのパッケージです。  
本パッケージは[zaki0929/raspimouse_game_controller](https://github.com/zaki0929/raspimouse_game_controller)をベースに開発されています。

## 動作環境

以下の環境にて動作確認を行っています。

* Raspberry Pi
  * Raspberry Pi 4 model B
* Ubuntu
  * Ubuntu 20.04
* ROS
  * ROS Noetic Ninjemys
* ROS Package
  * Raspberry Pi Cat Controller - [rt-net/raspicat_ros](https://github.com/rt-net/raspicat_ros)
  * yocs_velocity_smoother - [yujinrobot/yujin_ocs](https://github.com/yujinrobot/yujin_ocs)
  * joystick_drivers - [ros-drivers/joystick_drivers](https://github.com/ros-drivers/joystick_drivers)

## インストール

まずはじめに、[rt-net/raspicat_ros](https://github.com/rt-net/raspicat_ros)の[README](https://github.com/rt-net/raspicat_ros/blob/kinetic-devel/README.md)を参照してROSのセットアップとRaspberry Pi Cat制御用ROSパッケージのインストールを完了させてください。

* 以下のコマンドで本リポジトリをROSのワークスペースにダウンロードします。

```
cd ~/catkin_ws/src
git clone https://github.com/rt-net/raspicat_gamepad_controller.git
```

* 以下のコマンドで依存関係にあるパッケージをまとめてインストールします。

```
cd ~/catkin_ws
rosdep update
rosdep install -r -y --from-paths --ignore-src ./.
```

* 以下のコマンドでパッケージをビルドします。

```
cd ~/catkin_ws
catkin_make
source ~/catkin_ws/devel/setup.bash
```

## 使用方法

以下のコマンドをraspicat側で実行します。以下のコマンドを自分のpc側で実行し`joy`ノードを起動します。
```
$ roslaunch raspaicat raspicat.launch
```
以下のコマンドを自分のpc側で実行し`joy`ノードを起動します。
```
$ roslaunch raspicat_gamepad_controller logicool_cmd_vel.launch
```

ジョイスティックが`/dev/input/js0`以外のデバイスで認識されている（例えば`/dev/input/js1`）の場合、
以下のようにして起動するデバイスを指定できます。
```
$ roslaunch raspicat_gamepad_controller logicool_cmd_vel.launch dev:=/dev/input/js1
```

## 操作方法

まずはじめに、コントローラのモード切替スイッチを __DirectInput__ (D) modeに切り替え、MODEボタンの横のLEDが点灯していることを確認します。

Aボタン（緑）を押しながら十字ボタンを押すと上下で移動方向（前後）の指定、左右で旋回方向（左右）の指定ができます。 

Bボタン（赤）を押すと直進し、Yを押すと機体が停止します。

直進している時にでRスティックを左右に傾けると小さく曲がり、Lスティックを左右に傾けると大きく曲がります。

## ライセンス

各ファイルはライセンスがファイル中に明記されている場合、そのライセンスに従います。特に明記されていない場合は、The 3-Clause BSD Licenseに基づき公開されています。  
ライセンスの全文は[LICENSE](./LICENSE)または[https://opensource.org/licenses/BSD-3-Clause](https://opensource.org/licenses/BSD-3-Clause)から確認できます。

* [zaki0929/raspimouse_game_controller](https://github.com/zaki0929/raspimouse_game_controller)
    * [BSD 3-Clause License](https://github.com/zaki0929/raspimouse_game_controller/blob/master/LICENSE)
    * `Copyright (c) 2017, Ryo Okazaki`
