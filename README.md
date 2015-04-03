# Introduction
This module implements 'timed' loops with the pattern ``function(i) -> sleep(delay) ->function(i+1)``.
This project is in works-for-me status.

# Usage
    
    > -- new timed loop with timer-id 3
    > l = require('loop').new(3)

    > function derp(i)
    >     print("derp: "..i.." id: "..l:get_tmr_id())
    > end

    > function yay(i)
    >     print("finished yay! "..i)
    > end

    > -- start the loop, count from 1 to 10, increment 1, delay of 1000ms
    > l:loop(1,10,1,1000,derp)

    > -- use another timer,change the timer id of the current timer
    > tmr.alarm(4,2000,function () l:set_tmr_id(4) end )

    > -- register 'end' callback
    > l:on_finished(yay)
    > -- stop timer after 3.5 seconds, 
    > -- end callback will be executed with the last counter
    > tmr.alarm(5,3500,function () l:stop() end )
    > -- Output:
    derp: 1 id: 3
    derp: 2 id: 3
    derp: 3 id: 3
    derp: 4 id: 4
    derp: 5 id: 4
    finished yay! 5

