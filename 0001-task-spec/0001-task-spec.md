# OSS: 0001, Task format specification

 * Status: Draft

```
-type xpu() :: <<"cpu">> | <<"nvidia">> | <<"amd">>.

-type step() :: #{
    <<"name">>    => binary(),
    step_module() := step_args()
}.

-type step_module() ::
    <<"upload">> |
    <<"fetch">>  |
    <<"exec">>   |
    <<"pause">>.

-type step_args() ::
    step_upload_args() |
    step_fetch_args()  |
    step_exec_args()   |
    step_pause_args().

-type step_upload_args() :: #{
    <<"ttl">>   => non_neg_integer(),
    <<"files">> := [binary()]
}.

-type step_fetch_args() :: #{
    <<"files">> := [binary()],
    <<"dest">>  := binary()
}.

-type step_exec_args() :: #{
    <<"command">>       := binary() | [binary()],
    <<"ignore_errors">> => boolean(),
    <<"fetch_logs">>    => boolean()
}.

-type step_pause_args() :: #{
    <<"value">> := pos_integer()
}.

-type task() :: #{
    <<"name">>                   => binary(),
    <<"xpu">>                    := xpu(),
    <<"xpu-cpu-fallback">>       := boolean(),
    <<"xpu-n">>                  := pos_integer(),
    <<"xpu-fallback-wait-time">> => pos_integer(),
    <<"pending-ttl">>            => pos_integer(),
    <<"ttl">>                    => pos_integer(),
    <<"spaces">> := #{
        xpu() := binary()
    },
    <<"steps">> := [step()]
}.
```
