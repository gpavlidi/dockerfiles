# wine
Some random wine configuration. Not used for anything yet.

### Usage

After **docker pull gpavlidi/wine**, this alias in a bash_profile might come in handy:

- wine: dsfsd sdfsdf sdf
```
alias clingx="defaults write org.macosforge.xquartz.X11 enable_iglx -bool true && xhost + $(dinghy ip) && ip=$(ifconfig vboxnet0 | grep inet | awk '$1=="inet" {print $2}') && docker run -it --rm -e DISPLAY=${ip}:0 -v /tmp/.X11-unix:/tmp/.X11-unix --entrypoint=bash gpavlidi/wine"

```

Interesting wine dockers:

https://hub.docker.com/r/zcube/wine/~/dockerfile/
    su -p -l wine -c 'xvfb-run -a ./winetricks -q mfc40' && \
    su -p -l wine -c 'xvfb-run -a ./winetricks -q mfc42' && \
    su -p -l wine -c 'xvfb-run -a ./winetricks -q msvcirt' && \
    su -p -l wine -c 'xvfb-run -a ./winetricks -q python26' && \
    su -p -l wine -c 'xvfb-run -a ./winetricks -q vcrun6' && \
    su -p -l wine -c 'xvfb-run -a ./winetricks -q vcrun2010' && \
    su -p -l wine -c 'xvfb-run -a ./winetricks -q vcrun2013' && \
    su -p -l wine -c 'xvfb-run -a ./winetricks -q vcrun2015'

https://hub.docker.com/r/project5/wine/~/dockerfile/
	# Generate wine settings, waiting for wineserver to finish
	RUN xvfb-run wine "wineboot" && while pgrep -u `whoami` wineserver > /dev/null; do sleep 1; done


defaults write org.macosforge.xquartz.X11 enable_iglx -bool true && xhost + $(dinghy ip) && ip=$(ifconfig vboxnet0 | grep inet | awk '$1=="inet" {print $2}') && docker run -it --rm -v ${PWD}:/root/mount -e LIBGL_ALWAYS_INDIRECT=1 -e DISPLAY=${ip}:0 -v /tmp/.X11-unix:/tmp/.X11-unix --entrypoint=bash --name=wine gpavlidi/wine 

docker build --force-rm -t gpavlidi/wine .


apt-get install mingw-w64 git cmake
winetricks dotnet452 corefonts
git clone --depth 1 https://github.com/opentrack/LibOVR libOVR


i686-w64-mingw32-gcc ./hello.c -o hello32.exe
x86_64-w64-mingw32-gcc ./hello.c -o hello64.exe

# test it out
echo -e "#include <stdio.h>\nint main(){printf(\"Hello World\");return 0;}" > test.c
i686-w64-mingw32-gcc test.c -o test32.exe
x86_64-w64-mingw32-gcc test.c -o test64.exe


# to avoid below use:
LIBGL_ALWAYS_INDIRECT=1
libGL error: No matching fbConfigs or visuals found
libGL error: failed to load driver: swrast

fixme:win:EnumDisplayDevicesW ((null),1,0x23f200,0x00000000), stub!


winetricks windowscodecs corefonts dotnet20 dotnet4­0­­ 

WIN32 winetricks -q windowscodecs corefonts
WIN32 winetricks -q dotnet20 dotnet40
mkdir -p /mnt/vsexpress
mount -o loop VS2010Express1.iso /mnt/vsexpress/
mount VS2010Express1.iso /mnt/vsexpress/ -t iso9660 -o loop


WIN32 winetricks -q dotnet20
apt-get update
apt-get install winbind
WIN32 winetricks -q windowscodecs corefonts dotnet20


mkdir /mnt/vsc
mount -o loop ./VC.iso /mnt/vsc/


on codeblocks:
~/.config/codeblocks/default.conf
<compiler>
        <NON_PLAT_COMP bool="1" />

# replace all VS files IN-PLACE!!!
find . -name "*.sln" -o -name "*.vcxproj" -print0 | xargs -0 -n 1 sed -i "s/\\\/\//g"


WIN32 winetricks -q windowscodecs corefonts dotnet20 dotnet40 winhttp vc2010express

apt-get install p7zip-full winbind
7z x vs2010Express.iso
wine setup.exe /q
./vcssetup.exe
curl -L go.microsoft.com/?linkid=9709969 -o vs2010.iso

# http://www.orbiterwiki.org/wiki/Free_Compiler_Setup_Under_Linux

# after install get ome symlinks in place
cd ~/.wine32/drive_c
ln -s Program\ Files/Microsoft\ Visual\ Studio\ 10.0/VC
ln -s Program\ Files/Microsoft\ Platform\ SDK psdk
cd ~/.wine32/drive_c/windows/system32
ln -s ../../Program\ Files/Microsoft\ Visual\ Studio\ 10.0/Common7/IDE/mspdb100.dll

cp ~/.wine32/drive_c/Program\ Files/Microsoft\ Visual\ Studio\ 10.0/Common7/IDE/mspdbsrv.exe ~/.wine32/drive_c/VC/bin/
cp ~/.wine32/drive_c/Program\ Files/Microsoft\ Visual\ Studio\ 10.0/Common7/IDE/mspdb100.dll ~/.wine32/drive_c/VC/bin/
cp ~/.wine32/drive_c/Program\ Files/Microsoft\ Visual\ Studio\ 10.0/Common7/IDE/mspdbcore.dll ~/.wine32/drive_c/VC/bin/
cp ~/.wine32/drive_c/Program\ Files/Microsoft\ Visual\ Studio\ 10.0/Common7/IDE/mspdbst.dll ~/.wine32/drive_c/VC/bin/
cp ~/.wine32/drive_c/Program\ Files/Microsoft\ Visual\ Studio\ 10.0/Common7/IDE/msobj100.dll ~/.wine32/drive_c/VC/bin/

mspdbsrv.exe
mspdb100.dll
mspdbcore.dll
mspdbst.dll

# create the wrapper scripts
mkdir -p ~/devel/bin/
echo -e "#"'!'"/bin/bash\n\n WINEARCH=win32 WINEPREFIX=/root/.wine32 wine c:/VC/bin/cl.exe /I\"c:/VC/include\" /I\"c:/psdk/Include\" \$@" > ~/devel/bin/cl.sh
echo -e "#"'!'"/bin/bash\n\n WINEARCH=win32 WINEPREFIX=/root/.wine32 wine c:/VC/bin/link.exe /LIBPATH:\"c:/VC/lib\" /LIBPATH:\"c:/psdk/Lib\" \$@" > ~/devel/bin/link.sh
echo -e "#"'!'"/bin/bash\n\n WINEARCH=win32 WINEPREFIX=/root/.wine32 wine c:/VC/bin/rc.exe /I\"c:/VC/include\" /I\"c:/psdk/Include\" \$@" > ~/devel/bin/rc.sh
chmod +x ~/devel/bin/*

# serious bash hacking
# http://stackoverflow.com/questions/1853946/getting-the-last-argument-passed-to-a-shell-script
# putting wine before the last param
mv /usr/bin/cb_console_runner /usr/bin/cb_console_runner_ORIGINAL
echo -e "#"'!'"/bin/bash\n\n /usr/bin/cb_console_runner_ORIGINAL \${@:1:\$# - 1} WINEARCH=win32 WINEPREFIX=/root/.wine32 wine \${@:\$#}" > /usr/bin/cb_console_runner 
chmod +x /usr/bin/cb_console_runner

# this is what is being executed
Executing: xterm -T test2 -e /usr/bin/cb_console_runner LD_LIBRARY_PATH=$LD_LIBRARY_PATH:. /root/test2/bin/Debug/test2  (in /root/test2/.)

cl.sh /nologo /W3  /Zi /D_DEBUG /MDd     /c main.c /Foobj/Debug/main.obj
link.sh /nologo /LIBPATH:"C:/Program Files/Microsoft Visual Studio 10.0/VC/lib" /out:bin/Debug/Test msvcrtd.lib msvcprtd.lib obj/Debug/main.obj  /DEBUG


~/.config/codeblocks/default.conf


if (!platform::windows)
        {
            wxString shell = Manager::Get()->GetConfigManager(_T("app"))->Read(_T("/console_shell"), DEFAULT_CONSOLE_SHELL);
            cmd->command = shell + _T(" '") + cmd->command + _T("'");
        }



# add this define to solve 'GET_MODULE_HANDLE_EX_FLAG_FROM_ADDRESS' : undeclared identifier
#define _WIN32_WINNT 0x0501
