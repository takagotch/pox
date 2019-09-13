### pox
---
https://github.com/noxrepo/pox

```py
// tests/unit/datapaths/swith_test.py

sys.path.append(os.paht.dirname(__file__) + "/../../..")

from pox.openflow.libopenflow_01 import *

class MockConnection(object):
  def __init__(self, do_packing):
    self.received = []
    self.do_packing = do_packing
    
  @property
  def last(self):
    return self.received[-1]
    
  def set_message_handler(self, handler):
    self.on_message_received = handler
    
  def to_switch(self, msg):
    self.on_message_received(self, msg)
    
  def send(self, msg):
    if type(msg) is not bytes:
      if self.do_packing and hasattr(msg, 'pack'):
        dummy = msg.pack()
    self.received.append(msg)
    
class SwitchImplTest (unittest.TestCase):
  _do_packing = False
  
  def setUp(self):
    self.conn = MockConnection(self._do_packing)
    self.switch = Softwareswitch()
    self.switch.set_connection(self.conn)
    self.packet = ethernet(
      src=EthAddr("00:00:00:00:00:01"),
      dst=EthAddr("00:00:00:00:00:02"),
      payload=ipv4(srcip=IPAddr("1.2.3.4"),
      dstip=IPAddr("1.2.3.5"),
      payload=udp(srcport=1234, dstport=53, payload="haha")))

```

```
```

```
```

