# Intro
easy\_pause\_resume: Easy pause & resume a python program by sending signals.


# Install

```bash
pip install easy_pause_resume
```

# Usage

1. In your program where you may want to pause

  ```python
  ...
  import easy_pause_resume as epr
  ...

  def loop():
    ...
    while something:
      ...
      epr.wait_if_paused()
      ...
  ```

2. If you want to pause your program when it is running, execute `kill -SIGUSR1 <pid-of-your-program>`, and it will be blocked when `epr.wait_if_paused()` is executed in the future. `kill -SIGUSR2 <pid>` will bring it back to running where it paused. Without any signals, easy_pause_resume does nothing and won't block.
3. You can customize signals also

  ```python
  from easy_pause_resume import EasyPauseResume

  # using default signals: SIGUSR1 as pause and SIGUSR2 as resume
  epr = EasyPauseResume()
  epr.wait_if_paused()

  # using custom signals: SIGHUP as pause and SIGINT as resume
  epr = EasyPauseResume(sig_pause='SIGHUP', sig_resume='SIGINT')
  epr.wait_if_paused()

  # output logs
  epr = EasyPauseResume(debug=True)
  epr.wait_if_paused()
  ```
