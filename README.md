# Batch Files I use day to day and Implement in my tasks

I Prefer to download music in FLAC/WAV format but then I have to convert to listen them in my car!

### MP3 Converter
- To convert FLAC to 320k MP3 and then make a MP3 folder and move all the files inside.

  ```bat
  @echo off

  FOR /F "tokens=*" %%G IN ('dir /b *.flac') DO (ffmpeg -i "%%G" -ab 320k -map_metadata 0 -id3v2_version 3 "%%~nG.mp3")

  mkdir MP3

  FOR /F "tokens=*" %%G IN ('dir /b *.mp3') DO (move "%%G" "%CD%\MP3\")

  @pause
  
- To convert WAV to 320k MP3 and then make a MP3 folder and move all the files inside
  ```bat
  @echo off


  FOR /F "tokens=*" %%G IN ('dir /b *.wav') DO (ffmpeg -i "%%G" -vn -ar 44100 -ac 2 -b:a 320k "%%~nG.mp3")

  mkdir MP3

  FOR /F "tokens=*" %%G IN ('dir /b *.mp3') DO (move "%%G" "%CD%\MP3\")

  @pause

### To make streambable Hotstar cricket match links

- Hotstar live streaming is very useful and currently there is no DRM protection by them, so by network inspection you can generate links and copy paste in MXplayer/VLC streaming to play!

  ```bat
  @echo off
  
  echo.
  set /p id="Enter the ip adress:"
  (echo Copy paste in MX player stream, Enjoy :)
  echo.
  echo ::360p::
  echo. 
  echo %id%^master_1.m3u8^|user-agent=KAIOS/2.0
  echo.
  echo ::480p::
  echo. 
  echo %id%^master_2.m3u8^|user-agent=KAIOS/2.0
  echo.
  echo ::720p::
  echo. 
  echo %id%^master_3.m3u8^|user-agent=KAIOS/2.0
  echo.
  echo ::1080p::
  echo. 
  echo %id%^master_4.m3u8^|user-agent=KAIOS/2.0)
  
  @pause
  
- PS: To stream in VLC -> Show more options -> Edit Options -> :http-user-agent=KAIOS/2.0 in place of *user-agent=KAIOS/2.0*

### I Have to take streaming from IP camera and then create Screenshots
- I used FFMPEG to make this working:
  ```bat
  @echo off
 
  echo ~~~~For Video Capture~~~~
                                                                                       
  set /p id="Enter the IP adress:"
  set /p id2="Enter the duration in seconds:"
  set /p id3="Enter video name:"

  ffmpeg -i %id% -c:v copy -t %id2% %id3%.mp4

  @echo off
  echo ~~~~For Image Capture~~~~

  set /p id="Enter the video name:"
  set /p id2="Enter the number of frames/images you want:"
  set /p id3="Enter the total duration of video in seconds:"
  set /p id4="Enter of number of digits in images, example: Percentage03d :"

  ffmpeg -i %id%.mp4 -vf fps=%id2%/%id3% img%id4%.jpg
  
  @pause
  
