# Bashrecipies



#Oneliners og små funktioer der kan redde liv, hvis det foreksempel afhænger af om du skal optage noget fra P1 eller sådan noget i en fart


#Optag fra nuværende lydkilde

parec --monitor-stream=$(pacmd list-sink-inputs | grep -A 15 -B 3 RUNNING | grep index | rev | cut -d ' ' -f 1 | rev | grep -v 0 ) |  ffmpeg -f s16le -ar 44.1k -ac 2 -i pipe: ~/$(date +%s).mp3


#Download the song your'e listening to on youtube via firefox to a folder called /Musik/FraTuben

youtube-dl -o ~/Musik/FraTuben/'%(title)s.%(ext)s' -x --audio-format mp3 --prefer-ffmpeg $(lz4jsoncat ~/.mozilla/firefox/*.default-release/sessionstore-backups/recovery.jsonlz4 | jq -r ".windows[].tabs | sort_by(.lastAccesed)[] | .entries[.index-1] | .url" | grep youtube);


#How to acces the com port for extracting files from a digital theodolit or likewise

sudo chmod /dev/ttyUSB0 755
stty -F /dev/ttyUSB0 cs7 cstopb -ixon raw speed 9600
cat /dev/ttyUSB0

#Dump your browsinghistory with details

cp ~/.mozilla/firefox/*default-release/places.sqlite tmp.sqlite
sqlite3 tmp.sqlite .dump
rm -rf tmp.sqlite


#Cat all executable


ls -g | grep  ^-........x | rev | cut -d ' ' -f 1 | rev | while read a; do printf ${a} ; cat $a; done



#get the keymap for editining
xkbcomp -xkb $DISPLAY xkbmap
#Save a keymap you just editied, can be put into the .bashrc
xkbcomp -w 0 xkbmap $DISPLAY
