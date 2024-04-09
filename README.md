# potplayer-avisynth
potplayey avisynth frame interpolation 144hz

```
LoadPlugin("C:\Program Files (x86)\AviSynth+\plugins64\mvtools2.dll")
LoadPlugin("C:\Program Files (x86)\AviSynth+\plugins64\masktools2.dll")
Import("C:\Program Files (x86)\AviSynth+\scripts\Zs_RF_Shared.avsi")
Import("C:\Program Files (x86)\AviSynth+\scripts\SMDegrain v.3.1.2d.avsi")
SetMemoryMax(2048)
SetFilterMTMode("DEFAULT_MT_MODE", 2)
SetFilterMTMode("FFVideoSource", 3)
potplayer_source()
super=MSuper(pel=1, hpad=16, vpad=16,rfilter=4)
backward_1=MAnalyse(super, chroma=true, isb=true, blksize=16, search=3, searchparam=5, delta= 1, truemotion=true, plevel=0, badrange=(24))
forward_1=MAnalyse(super, chroma=true, isb=false, blksize=16, search=3, searchparam=5, delta= 1, truemotion=true, plevel=0, badrange=(24))
backward_2 = MRecalculate(super, chroma=true, backward_1, blksize=16, searchparam=3, search=3)
forward_2 = MRecalculate(super, chroma=true, forward_1, blksize=16, searchparam=3, search=3)

MDegrain2(super, backward_1, forward_1, backward_2, forward_2)

MFlowFps(super , backward_2, forward_2, num=0, den=1)
Prefetch(12)
```
