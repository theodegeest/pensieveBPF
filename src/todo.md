# TODO list

- when unscheduling look at state

 `TASK_RUNNING`          runnable or currently running if scheduled out: cause preemption
 `TASK_INTERRUPTIBLE`    sleeping (can be woken by signal) sleep, futex, yield
 `TASK_UNINTERRUPTIBLE`  waiting for I/O / lock (lock? maybe lookup)
 `TASK_STOPPED`          stopped by signal
 `TASK_DEAD`             exiting

- put a probe on the userspace mutex
  This makes it possible to distinguish a lock that unscheduled from a yield
  Also now a spinlock is detected!
  maybe futex? But the unschedule already tells us it has called the futex_wait
    tracepoint/syscalls/sys_enter_futex
    tracepoint/syscalls/sys_exit_futexsched_switch

    tracepoint/lock/lock_acquire
    tracepoint/lock/lock_release

- IO
  sys_enter_read (userspace read)
  block_rq_issue (start an io)
  block_rq_complete (io is complete?)
  sched_switch (maybe schedule back? before or after complete?)

- yield?
  tracepoint/syscalls/sys_enter_sched_yield

- sleep?
  tracepoint/syscalls/sys_enter_nanosleep

- add synchronisation metric (contention?)
- add syscall metric
- add memory metric (LLC?)
- Make user side request latest data when closing (to reduce information loss on last profile block)
