# ð¥11 NATì í¬í¸í¬ìë©

## NAT(Network Address Translation)ë?

- IP í¨í·ì ìë ì¶ë°ì§ ë° ëª©ì ì§ì IP ì£¼ìì TCP/UDP í¬í¸ ì«ì ë±ì ë°ê¿ ì¬ê¸°ë¡íë©´ì ë¤í¸ìí¬ í¸ëí½ì ì£¼ê³  ë°ê² íë ê¸°ì 

  -> í¹ì  ipì£¼ìì í¹ì  í¬í¸ë²í¸ë¡ ê°ë í¨í·ì ë¤ë¥¸ ipì£¼ìì ë¤ë¥¸ í¬í¸ë²í¸ë¡ ë°ê¿ì£¼ë ê²

- í¨í·ì ë³íê° ìê¸°ê¸° ëë¬¸ì, IPë TCP/UDPì ì²´í¬ì¬ë ë¤ì ê³ì°ëì´ ì¬ê¸°ë¡í´ì¼ íë¤.

- ì£¼ë¡ ì¬ì¤ ë¤í¸ìí¬ì ìí ì¬ë¬ ê°ì í¸ì¤í¸ê° íëì ê³µì¸ IP ì£¼ìë¥¼ ì¬ì©íì¬ ì¸í°ë·ì ì ìíê¸° ìí´ ì¬ì©íë¤.

- íì§ë§, ê¼­ ì¬ì¤IPë¥¼ ê³µì¸ IPë¡ ë³ííë ë°ìë§ ì¬ì©íë ê¸°ì ì ìëë¤.



### ð¤ NATë¥¼ ì¬ì©íë ì´ì ?

- IP ì£¼ì ì ì½ê³¼ ë³´ì
  - íëì ê³µì¸ IP ì£¼ìë¥¼ ì¬ì©íì¬ ì¬ë¬ ëì í¸ì¤í¸ê° ì¸í°ë·ì ì ìí  ì ìë¤. ìëíë©´ ì¸í°ë· ê³µì ê¸°ì NAT ê¸°ë¥ì´ íì¬ëì´ ìê¸° ëë¬¸ì´ë¤. ë°ë¼ì ë¶ì¡±í ê³µì¸ IPë¥¼ ì ì½í  ì ìë¤.
  - NAT ëìì í¹ì±ì IPë¥¼ ì¨ê¸¸ ì ìë ê¸°ë¥ì´ ìë¤. ìë¥¼ ë¤ì´ì, ë¼ì°í°(ê³µì ê¸°) ì¸ë¶ë¡ í¸ëí½ì´ ëê° ëë ì¬ì¤ IPê° ê³µì¸ IPì£¼ìë¡ ë°ëë¯ë¡ ê³µê²©ìê° ë¼ì°í° ì ìª½ì ìë ì¬ì¤ IPë¥¼ ëª¨ë¥´ê¸° ëë¬¸ì ìµì¢ ëª©ì ì§ë¡ì ê³µê²©ì´ ì´ë ¤ìì ¸ì ë´ë¶ ë¤í¸ìí¬ ë° í¸ì¤í¸ë¤ì ë³´í¸í  ì ìë¤.



### ð¤ NAT ëì ìë¦¬

ë§ì½ ì¸ë¶ì ìë ì¹ ìë²ë¡ ì ê·¼íê³ ì í  ë í´ë¹ ìì²­ í¨í·ì ë°ëì í´ë¹ ê²ì´í¸ì¨ì´(ê³µì ê¸°)ë¥¼ ê±°ì¹ê² ëë¤. ì´ ë, ê²ì´í¸ì¨ì´(ê³µì ê¸°)ì ì´ë¤ ë¤í¸ìí¬ê° ì´ëë¡ ê°ëì§ì ëí ê¸°ë¡ì´ ì ì¥ëë¤.

![nat1](img/NAT/nat1.png)

![nat2](img/NAT/nat2.png)

1. í¨í· í¤ëì ì¶ë°ì§ì ëª©ì ì§ì ì£¼ìë¥¼ ê¸°ë¡íë¤.(ì¶ë°ì§ë ìì ì ì¬ì¤ë§ IPì£¼ìë¥¼ ê¸°ë¡íë¤.)

   > ì¶ë°ì§ IP ì£¼ì: 10.0.0.1
   >
   > ëª©ì ì§ IP ì£¼ì: 300.0.0.1

   

2. ê¸°ë³¸ ê²ì´í¸ì¨ì´(ê³µì ê¸°) ììë ì¸ë¶ë¡ ëê°ë í¨í·ì ì¸ìíê² ëë©´, ì¶ë°ì§ì IPì£¼ìë¥¼ ê²ì´í¸ì¨ì´ ìì ì ê³µì¸ IP ì£¼ìë¡ ë³ê²½íë¤. ì´ ë, ë³ëì NAT íì´ë¸ì ë³´ê´íë¤.

   > ì¶ë°ì§ IP ì£¼ì: 10.0.0.1 -> 200.0.0.1 (ì¬ê¸°ë¡)
   >
   > ëª©ì ì§ IP ì£¼ì: 300.0.0.1

   | íë¡í ì½ | ì¬ì¤IP   | ì¶ë°ì§ IP | ëª©ì ì§ IP |
   | -------- | -------- | --------- | --------- |
   | TCP      | 10.0.0.1 | 200.0.0.1 | 300.0.0.1 |

   

3. ì¹ ìë²ìì ìì í ë°ì´í° ì²ë¦¬ í, ìëµí¨í·ì ë³´ë´ëë° ë¤ìê³¼ ê°ì´ ë³´ë´ì§ë¤.

   > ì¶ë°ì§ IP ì£¼ì: 300.0.0.1
   >
   > ëª©ì ì§ IP ì£¼ì: 200.0.0.1

   

4. í¸ì¤í¸ì ê²ì´í¸ì¨ì´ìì ì¹ ìë²ê° ë³´ë¸ í¨í·ì ë°ì¼ë©´, NAT íì´ë¸ì ì°¸ê³ í´ì í¸ì¤í¸ì ì¬ì¤ IPë¡ í¨í·ì ì ë¬íë¤.

   > ì¶ë°ì§ IP ì£¼ì: 300.0.0.1
   >
   > ëª©ì ì§ IP ì£¼ì: 10.0.0.1 

   



## í¬í¸í¬ìë©

- í¨í·ì´ ë¼ì°í°ë ë°©íë²½ê³¼ ê°ì ë¤í¸ìí¬ ê²ì´í¸ì¨ì´ë¥¼ ê°ë¡ì§ë¥´ë ëì íëì IPì£¼ìì í¬í¸ ë²í¸ ê²°í©ì íµì  ìì²­ì ë¤ë¥¸ ê³³ì¼ë¡ ëê²¨ì£¼ë NATì ìì© ê¸°ì 

- ìê²© ì»´í¨í°ê° ê·¼ê±°ë¦¬ íµì ë§(LAN) ë´ì ìì¹í í¹ì  ì»´í¨í°ë ìë¹ì¤ì ì°ê²°í  ë ì¬ì©íë¤.



1. ë³´ì´ì§ ìë ì¬ì¤ ë¤í¸ìí¬ ëì­ì ìë ë¬´ì¸ê°ì íµì ì íê³  ì¶ì ë

   ![í¬í¸í¬ìë©1](img/NAT/%ED%8F%AC%ED%8A%B8%ED%8F%AC%EC%9B%8C%EB%94%A91.PNG)

2. ì§ì  ëª©ì ì§ ipì í´ë¹ ì»´í¨í°ì IPë¥¼ ë£ë ê²ì´ ìëë¼, ê³µì¸ IPë¡ ì¤ì íì¬ ë³´ë¸ë¤.

   -> í´ë¹ ê³µì ê¸°ì í¬í¸í¬ìë© ì¤ì ì í´ëìì¼ íë¤.

   ![í¬í¸í¬ìë©2](img/NAT/%ED%8F%AC%ED%8A%B8%ED%8F%AC%EC%9B%8C%EB%94%A92.png)

3. í¨í·ì ë°ì ê³µì ê¸°ë ë´ë¶ ë¤í¸ìí¬ ëì­ìì í¹ì  IPì í¹ì  í¬í¸ë¡ ì ì¡íë¤.

   ![í¬í¸í¬ìë©3](img/NAT/%ED%8F%AC%ED%8A%B8%ED%8F%AC%EC%9B%8C%EB%94%A93.png)

