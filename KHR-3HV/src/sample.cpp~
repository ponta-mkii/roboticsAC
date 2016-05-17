// URDFモデルを動かすプログラム
#include <string>
#include <ros/ros.h>
#include <sensor_msgs/JointState.h>
#include <tf/transform_broadcaster.h>

int main(int argc, char** argv) {
  ros::init(argc, argv, "ノード名");                 // ROSの初期化
  ros::NodeHandle nh;                                // ノードハンドルの生成

  ros::Publisher pub = nh.advertise<sensor_msgs::JointState>("joint_state", 1);  // ジョイント角度送信要publisher生成
  tf::TransfromBroadCaster tbc;                      // 位置送信用broadcaster生成

  geometry_msgs::TransformStamped tsm;               // ロボットの位置を格納するメッセージ
  sensor_msgs::JointState jsm;                       // ロボットのジョイント角度を格納するメッセージ
  tsm.header.frame.id = "ベースフレーム名";          // 全ての変換はこのベースフレームを参照して行われる。
  tsm.child_frame_id = "ベースリンク名";             // ロボットのベースとなるリンクを設定

  // 以下ではロボットのジョイント数をnとしている。
  // ジョイント用メッセージの初期化
  jsm.name.resize(n);                                // ジョイント数によりメッセージサイズを設定
  tsm.position.resize(n);
  jsm.name[0] = "ジョイント0名";                     // ジョイント0の名前設定
           :
  jsm.name[n-1] = "ジョイントn-1名";                 // ジョイントn-1の名前設定

  (ここにロボットジョイント角度、位置用変数の定義と初期化処理を入れる。)

  // 一定周期の無限ループ処理
  ros::Rate rate(10);                                // 送信周期設定（10Hz)
  while(ros::ok()) {                                 // 「Ctrl+C」が押されるまで無限ループ
    // ロボットジョイント角度の設定
    jsm.header.stamp = ros::Time::now();             // ジョイントのメッセージに送信時間を設定
    jsm.position[0] = ジョイント0角度;               // ジョイント0の角度をメッセージに設定
           :
    jsm.position[n-1] = ジョイントn-1角度;           // ジョイントn-1の角度をメッセージに設定

    // ロボット位置・角度の設定
    tsm.header.stamp = ros::Time::now();             // ロボット位置のメッセージに送信時間を設定
    tsm.transform.translation.x = ロボット位置x;     // ロボット位置Xをメッセージに設定
    tsm.transform.translation.y = ロボット位置y;     // ロボット位置Yをメッセージに設定
    tsm.transform.translation.z = ロボット位置z;     // ロボット位置Zをメッセージに設定
    tsm.transform.rotation = tf::createQuaternionMsgFromYaw(ロボットが向いている角度);  // Yaw角をクォータニオンへ変換

    // ロボットジョイント、位置・角度の発行
    pub.publish(jsm);                                // ジョイント角メッセージを送信
    tbc.sendTransform(tsm);                          // ロボット位置メッセージ送信

    （ここにロボットジョイント角度、位置・角度の更新処理を入れる。）

    rate.sleep();                                    // 設定時間スリープ
  }
  return 0;
}
