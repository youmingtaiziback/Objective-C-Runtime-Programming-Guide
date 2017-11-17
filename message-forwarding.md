# Message Forwarding {#pageTitle}

给一个对象发送处理不了的消息会发生错误，但在此之前，运行时系统给了对象处理消息的机会

## Forwarding

向一个对象发送了处理不了的消息时，在发生错误之前，运行时会向对象发送forwardInvocation:消息并附带唯一的参数NSInvocation对象，该对象封装了原始的方法和参数



