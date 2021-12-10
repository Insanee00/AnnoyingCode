:a
:: usage:
::   beep           -- beeps immediately
::   beep 1         -- beeps after 1 sec
::   beep 1:2       -- beeps after 1 min,  2 sec
::   beep 1:2:3     -- beeps after 1 hour, 2 min,   3 sec
::   beep 1:2:3:4   -- beeps after 1 day,  2 hours, 3 min, 4 sec
::
:: invalid usages:
::    beep 1::2
::    beep :1
::    beep 1:
::    beep :1:

@echo off

set part1=
set part2=
set part3=
set part4=

for /f "tokens=1-4 delims=:" %%a in ("%1") do ^
set part1="%%a"& ^
set part2="%%b"& ^
set part3="%%c"& ^
set part4="%%d"

if not x%part4%==x"" (
	sleep %part1%d %part2%h %part3%m %part4%s
) else (
	if not x%part3%==x"" (
		sleep %part1%h %part2%m %part3%s
	) else (
		 if not x%part2%==x"" (
			sleep %part1%m %part2%s
		) else (
			if not x%part1%==x"" sleep %part1%s
		)
	)
)

echo 
goto :a