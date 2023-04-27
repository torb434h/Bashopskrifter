# Bashopskrifter
Snusfornuftige husmorråd


#Oneliners og små funktioer der kan redde liv, hvis det foreksempel afhænger af om du skal optage noget fra P1 eller sådan noget i en fart


#Optag fra nuværende lydkilde

parec --monitor-stream=$(pacmd list-sink-inputs | grep -A 15 -B 3 RUNNING | grep index | rev | cut -d ' ' -f 1 | rev | grep -v 0 ) |  ffmpeg -f s16le -ar 44.1k -ac 2 -i pipe: ~/$(date +%s).mp3


#Download den sang du hører fra youtube gennem firefox og download den til en mappe der hedder /Musik/FraTuben

youtube-dl -o ~/Musik/FraTuben/'%(title)s.%(ext)s' -x --audio-format mp3 --prefer-ffmpeg $(lz4jsoncat ~/.mozilla/firefox/*.default-release/sessionstore-backups/recovery.jsonlz4 | jq -r ".windows[].tabs | sort_by(.lastAccesed)[] | .entries[.index-1] | .url" | grep youtube);

#Dump din internethistorik 4realz

cp ~/.mozilla/firefox/*default-release/places.sqlite tmp.sqlite
sqlite3 tmp.sqlite .dump
rm -rf tmp.sqlite


#Cat alle eksekverbare filer i mappen 
ls -g | grep  ^-........x | rev | cut -d ' ' -f 1 | rev | while read a; do printf ${a} ; cat $a; done



#Hent keymap så man kan rette i det
xkbcomp -xkb $DISPLAY xkbmap
#Gem et keymap. kan evt puttes i .bashrc
xkbcomp -w 0 xkbmap $DISPLAY
