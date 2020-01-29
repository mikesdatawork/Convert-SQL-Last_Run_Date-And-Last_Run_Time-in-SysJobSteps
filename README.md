![MIKES DATA WORK GIT REPO](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_01.png "Mikes Data Work")        # Convert SQL Last_Run_Date And Last_Run_Time in SysJobSteps
**Post Date: June 30, 2015**





## Contents    
- [About Process](##About-Process)  
- [SQL Logic](#SQL-Logic)  
- [Build Info](#Build-Info)  
- [Author](#Author)  
- [License](#License)       

## About-Process


<p>If you found this post… You probably want to make more sense out of the last_run_date, and last_run_time columns from the msdb..sysjobsteps table. Here is a quick conversion for you. I did a basic conversion to formulate a date/time you could use in other functions. It's the "last run literal", then I converted again to extrapolate the Day name using the datename function, and then once more to get an abbreviated Month/Day/Year & time.</p>      



## SQL-Logic
```SQL
-- use this to get all step info about your job, and steps, including last run history.
select
 'job name' = sj.name
, 'step id' = sjs.step_id
, 'step name' = sjs.step_name
, 'last run literal' = dateadd(millisecond, sjs.last_run_time,convert(datetime,cast(nullif(sjs.last_run_date,0) as nvarchar(10))))
, 'last run day' = datename(dw, dateadd(millisecond, sjs.last_run_time,convert(datetime,cast(nullif(sjs.last_run_date,0) as nvarchar(10)))))
, 'last run date' = convert(char, dateadd(millisecond, sjs.last_run_time,convert(datetime,cast(nullif(sjs.last_run_date,0) as nvarchar(10)))), 9)
from
 msdb..sysjobs sj join msdb..sysjobsteps sjs on sj.job_id = sjs.job_id
order by
 sj.name, sjs.step_id asc
```

![Convert Last Run History]( https://mikesdatawork.files.wordpress.com/2015/06/image0017.jpg "Convert Run History In SysJobSteps")
 


[![WorksEveryTime](https://forthebadge.com/images/badges/60-percent-of-the-time-works-every-time.svg)](https://shitday.de/)

## Build-Info

| Build Quality | Build History |
|--|--|
|<table><tr><td>[![Build-Status](https://ci.appveyor.com/api/projects/status/pjxh5g91jpbh7t84?svg?style=flat-square)](#)</td></tr><tr><td>[![Coverage](https://coveralls.io/repos/github/tygerbytes/ResourceFitness/badge.svg?style=flat-square)](#)</td></tr><tr><td>[![Nuget](https://img.shields.io/nuget/v/TW.Resfit.Core.svg?style=flat-square)](#)</td></tr></table>|<table><tr><td>[![Build history](https://buildstats.info/appveyor/chart/tygerbytes/resourcefitness)](#)</td></tr></table>|

## Author

[![Gist](https://img.shields.io/badge/Gist-MikesDataWork-<COLOR>.svg)](https://gist.github.com/mikesdatawork)
[![Twitter](https://img.shields.io/badge/Twitter-MikesDataWork-<COLOR>.svg)](https://twitter.com/mikesdatawork)
[![Wordpress](https://img.shields.io/badge/Wordpress-MikesDataWork-<COLOR>.svg)](https://mikesdatawork.wordpress.com/)


## License
[![LicenseCCSA](https://img.shields.io/badge/License-CreativeCommonsSA-<COLOR>.svg)](https://creativecommons.org/share-your-work/licensing-types-examples/)

![Mikes Data Work](https://raw.githubusercontent.com/mikesdatawork/images/master/git_mikes_data_work_banner_02.png "Mikes Data Work")

