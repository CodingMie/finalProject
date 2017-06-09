----------------------------------------------------------------------------

TODO:
- GameScene
  - 谱面速度控制
  - GLOBAL类设置为单例模式
  - 敲击检测
  - 敲击监听
- SelectScene 目前什么都没实现
- ResultScene 目前什么都没实现


主要组成：
1.GameScene 游玩界面
2.SelectScene 选择界面
3.ResultScene 结果界面
4.一个管理全局办法的类Global
5.VisibleRect 用来设置各种位置的，目前是在类里设置一个实例使用

----------------------------------------------------------------------------

游玩逻辑：
update函数中按照谱面时间码和当前时间计数器的时
创造note
----------------------------------------------------------------------------
谱面使用的jsoncpp来写入的，不做谱面就不用装了。

【】谱面记录格式】
谱面结构：
{ "array": [   /*这里是一个实际谱面信息的数组*/] }

数组里面每一个元素都是这样的：
{
   "time" : 1896,  //  时间戳
   "tracks" : [    // 一个数组，包括每个轨道在这个时间戳会有什么note落下来
      {
         "length" : 1,   // note持续时间，主要是设计给长条用的
         "num" : 0,   // 轨道号码
         "type" : "tap"  // tap就是点一下
      },
      {
         "length" : 0,
         "num" : 1,
         "type" : "none" // none表示这个时刻这个轨道不会有note掉落
      },
      {
         "length" : 1,
         "num" : 2,
         "type" : "tap"
      },
      {
         "length" : 0,
         "num" : 3,
         "type" : "none"
      }
   ]
}
时间单位：10ms,即0.01s，因为设计为1ms的话刷新跟不上

----------------------------------------------------------------------------

一些代码参考  REF:

	this->runAction(Sequence::create(FadeOut::create(0.2f), DelayTime::create(0.2f),
  CallFunc::create(CC_CALLBACK_0(Note::removeNote, this)), NULL));//消失特效

  // 添加监听器
  void FriendShip::addListener() {
    auto keyboardListener = EventListenerKeyboard::create();
    keyboardListener->onKeyPressed = CC_CALLBACK_2(FriendShip::onKeyPressed, this);
    keyboardListener->onKeyReleased = CC_CALLBACK_2(FriendShip::onKeyReleased, this);
    _eventDispatcher->addEventListenerWithSceneGraphPriority(keyboardListener, this);

    auto contactListener = EventListenerPhysicsContact::create();
    contactListener->onContactBegin = CC_CALLBACK_1(FriendShip::onConcactBegin, this);
    _eventDispatcher->addEventListenerWithSceneGraphPriority(contactListener, this);
  }
