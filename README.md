----------------------------------------------------------------------------

TODO:
- GameScene
  - �����ٶȿ���
  - GLOBAL������Ϊ����ģʽ
  - �û����
  - �û�����
- SelectScene Ŀǰʲô��ûʵ��
- ResultScene Ŀǰʲô��ûʵ��


��Ҫ��ɣ�
1.GameScene �������
2.SelectScene ѡ�����
3.ResultScene �������
4.һ������ȫ�ְ취����Global
5.VisibleRect �������ø���λ�õģ�Ŀǰ������������һ��ʵ��ʹ��

----------------------------------------------------------------------------

�����߼���
update�����а�������ʱ����͵�ǰʱ���������ʱ
����note
----------------------------------------------------------------------------
����ʹ�õ�jsoncpp��д��ģ���������Ͳ���װ�ˡ�

���������¼��ʽ��
����ṹ��
{ "array": [   /*������һ��ʵ��������Ϣ������*/] }

��������ÿһ��Ԫ�ض��������ģ�
{
   "time" : 1896,  //  ʱ���
   "tracks" : [    // һ�����飬����ÿ����������ʱ�������ʲônote������
      {
         "length" : 1,   // note����ʱ�䣬��Ҫ����Ƹ������õ�
         "num" : 0,   // �������
         "type" : "tap"  // tap���ǵ�һ��
      },
      {
         "length" : 0,
         "num" : 1,
         "type" : "none" // none��ʾ���ʱ��������������note����
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
ʱ�䵥λ��10ms,��0.01s����Ϊ���Ϊ1ms�Ļ�ˢ�¸�����

----------------------------------------------------------------------------

һЩ����ο�  REF:

	this->runAction(Sequence::create(FadeOut::create(0.2f), DelayTime::create(0.2f),
  CallFunc::create(CC_CALLBACK_0(Note::removeNote, this)), NULL));//��ʧ��Ч

  // ��Ӽ�����
  void FriendShip::addListener() {
    auto keyboardListener = EventListenerKeyboard::create();
    keyboardListener->onKeyPressed = CC_CALLBACK_2(FriendShip::onKeyPressed, this);
    keyboardListener->onKeyReleased = CC_CALLBACK_2(FriendShip::onKeyReleased, this);
    _eventDispatcher->addEventListenerWithSceneGraphPriority(keyboardListener, this);

    auto contactListener = EventListenerPhysicsContact::create();
    contactListener->onContactBegin = CC_CALLBACK_1(FriendShip::onConcactBegin, this);
    _eventDispatcher->addEventListenerWithSceneGraphPriority(contactListener, this);
  }
