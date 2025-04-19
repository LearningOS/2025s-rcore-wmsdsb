1. 一些非法操作                      RISC-V SBI v1.0.0
2.  1.sp 指向内核栈中保存的用户态上下文，
    使用情景：1.正常Trap返回
            2.任务初次调度
    2.sstatus寄存器    恢复用户态时的 CPU 状态
      sepc，          用户态程序恢复后执行的指令地址
      scratch         保存用户态 sp
    3.x2（sp）：已在 csrrw sp, sscratch, sp 中单独处理（切换回用户栈）
      x4（tp）：通常用于线程局部存储（TLS）, 用户态和内核态共享该寄存器，无需恢复
    4.sp为用户栈指针
      sscratch保存了内核栈指针
    5.sret sret被写入pc,然后跳转回用户态代码，并且sstatus将为u态
    6.sp为内核栈指针，sscratch保存用户栈指针
    7.ecall