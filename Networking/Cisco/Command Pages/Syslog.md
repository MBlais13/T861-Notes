#Logs #Monitoring

> [!info] Commands
> [[Cisco Commands#Syslog]]

Whenever anything interesting is happening on your device, IOS informs us in real-time. This is done by syslog.

---
## About Syslog in IOS
By default, these syslog messages are only outputted to the console. This is because the **logging console** command is enabled by default. If you log in through telnet or SSH, you won’t see any syslog messages. You can enable this with the **terminal monitor** command.

```
S1(config)# logging console ?
  <0-7>          Logging severity level
  alerts         Immediate action needed           (severity=1)
  critical       Critical conditions               (severity=2)
  debugging      Debugging messages                (severity=7)
  discriminator  Establish MD-Console association
  emergencies    System is unusable                (severity=0)
  errors         Error conditions                  (severity=3)
  filtered       Enable filtered logging
  guaranteed     Guarantee console messages
  informational  Informational messages            (severity=6)
  notifications  Normal but significant conditions (severity=5)
  warnings       Warning conditions                (severity=4)
  xml            Enable logging in XML
```