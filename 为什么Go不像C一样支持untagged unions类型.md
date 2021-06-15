# 为什么Go不像C一样支持untagged unions类型?

因为untagged unions会破坏Go的内存安全机制。