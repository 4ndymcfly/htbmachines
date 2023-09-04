#!/bin/bash

# By 4ndyMcFly 2023
# Requires Nerd Fonts to display symbols correctly.
# Extended practice of the Hacking course by Hack4u (@S4vitar)
# English version

clear

#Colors
greenColor="\e[0;32m\033[1m"
endColor="\033[0m\e[0m"
redColor="\e[0;31m\033[1m"
blueColor="\e[0;34m\033[1m"
yellowColor="\e[0;33m\033[1m"
purpleColor="\e[0;35m\033[1m"

function ctrl_c(){
  echo -e "\n\n${redColor}[!]${endColor} Exiting...\n"
  tput cnorm && exit 1
}

# Ctrl+C
trap ctrl_c INT

# Global variables
main_url="https://htbmachines.github.io/bundle.js"

function helpPanel() {
  echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
  echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
  echo -e "\n\n${purpleColor}${endColor} Usage:\n ${blueColor}\t\t./htbmachines${endColor}${purpleColor} [OPTION]${endColor}\n"
  echo -e "${purpleColor}\t\t-The options -o (OS) and -d (DIFFICULTY) can be concatenated. \n\t\t Example: ${endColor}${blueColor}./htbmachines -o Linux -d Insane${endColor}\n"
  echo -e "${purpleColor}\t\t-The options -c (CERTIFICATION) and -d (DIFFICULTY) can be concatenated. \n\t\t Example: ${endColor}${blueColor}./htbmachines -c OSCP -d Easy${endColor}"
  echo -e "\n\n${purpleColor}${endColor} Options: \n"
  echo -e "\t${purpleColor}-u${endColor},\tUpdate/Download DB of machines."
  echo -e "\t${purpleColor}-m${endColor},\tSearch by machine name."
  echo -e "\t${purpleColor}-i${endColor},\tSearch by machine IP."
  echo -e "\t${purpleColor}-o${endColor},\tSearch by machine Operating System (Windows, Linux)."
  echo -e "\t${purpleColor}-s${endColor},\tSearch machines with the indicated Skill."
  echo -e "\t${purpleColor}-c${endColor},\tSearch machines by the indicated certification (OSCP, eJPT, etc)."
  echo -e "\t${purpleColor}-d${endColor},\tList available machines according to their difficulty (Easy, Medium, Hard, Insane)."
  echo -e "\t${purpleColor}-y${endColor},\tGet YouTube URL of the machine resolution."
  echo -e "\t${purpleColor}-h${endColor},\tShow this help panel.\n"
  echo -e "\n\n${purpleColor}${endColor} Note: \n\t\t${purpleColor}It is recommended to have Nerd Fonts installed to display symbols correctly."
  echo -e "\t\tYou can download them from https://www.nerdfonts.com/font-downloads.${endColor}\n\n"
}

function updateFiles(){
  tput civis

  if [ ! -f bundle.js ]; then
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${purpleColor}[󰁅]${endColor} Downloading files..."
    curl -s $main_url > bundle.js
    js-beautify bundle.js | sponge bundle.js
    echo -e "\n${greenColor}[✔]${endColor} Data downloaded successfully. You can start searching now.\n"
    tput cnorm
  else
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${purpleColor}[!]${endColor} Checking for updates, please wait..."
    curl -s $main_url > bundle_temp.js
    js-beautify bundle_temp.js | sponge bundle_temp.js
    sed -i 's/Fácil/Easy/g' bundle_temp.js
	sed -i 's/Media/Medium/g' bundle_temp.js
	sed -i 's/Difícil/Hard/g' bundle_temp.js
    md5_temp_value=$(md5sum bundle_temp.js | awk '{print $1}')
    md5_original_value=$(md5sum bundle.js | awk '{print $1}')

      if [ "$md5_original_value" == "$md5_temp_value" ]; then
        echo -e "\n${greenColor}[✔]${endColor} No new updates, you are up to date.\n"
        sleep 1
        rm bundle_temp.js
      else
        echo -e "\n${purpleColor}[󰁅]${endColor} New updates found, downloading..."
        sleep 2
        rm bundle.js && mv bundle_temp.js bundle.js
        echo -e "\n${greenColor}[✔]${endColor} Data updated successfully.\n"
      fi
    tput cnorm
  fi
}

function downloadDB(){
  tput civis
  echo -e "\n${purpleColor}[󰁅]${endColor} Downloading files..."
  curl -s $main_url > bundle.js
  js-beautify bundle.js | sponge bundle.js
  echo -e "\n${greenColor}[✔]${endColor} Data downloaded successfully. You can start searching now.\n"
  tput cnorm
}

function searchMachine(){
    machineName="$1"

    machineNameCheck="$(cat bundle.js | awk "BEGIN {IGNORECASE = 1} /name: \"$machineName\"/,/resuelta:/" | grep -vE "id:|sku:|resuelta:" | tr -d '"' | tr -d ',' | sed 's/^ *//')"

    if [ "$machineNameCheck" ]; then
        # Declare variables
        name="$(cat bundle.js | awk "BEGIN {IGNORECASE = 1} /name: \"$machineName\"/,/resuelta:/" | grep -vE "id:|sku:|resuelta:" | tr -d '"' | tr -d ',' | sed 's/^ *//' | grep "name:" | awk 'NF {print $NF}')"
        ip="$(cat bundle.js | awk "BEGIN {IGNORECASE = 1} /name: \"$machineName\"/,/resuelta:/" | grep -vE "id:|sku:|resuelta:" | tr -d '"' | tr -d ',' | sed 's/^ *//' | grep "ip:" | awk 'NF {print $NF}')"
        so="$(cat bundle.js | awk "BEGIN {IGNORECASE = 1} /name: \"$machineName\"/,/resuelta:/" | grep -vE "id:|sku:|resuelta:" | tr -d '"' | tr -d ',' | sed 's/^ *//' | grep "so:" | awk 'NF {print $NF}')"
        dificultad="$(cat bundle.js | awk "BEGIN {IGNORECASE = 1} /name: \"$machineName\"/,/resuelta:/" | grep -vE "id:|sku:|resuelta:" | tr -d '"' | tr -d ',' | sed 's/^ *//' | grep "dificultad: " | awk 'NF {print $NF}')"
        skills="$(cat bundle.js | awk "BEGIN {IGNORECASE = 1} /name: \"$machineName\"/,/resuelta:/" | grep -vE "id:|sku:|resuelta:" | tr -d '"' | tr -d ',' | sed 's/^ *//' | grep "skills:" | awk '{$1=""; print $0}')"
        like="$(cat bundle.js | awk "BEGIN {IGNORECASE = 1} /name: \"$machineName\"/,/resuelta:/" | grep -vE "id:|sku:|resuelta:" | tr -d '"' | tr -d ',' | sed 's/^ *//' | grep "like:" | awk '{$1=""; print $0}')"
        youtube="$(cat bundle.js | awk "BEGIN {IGNORECASE = 1} /name: \"$machineName\"/,/resuelta:/" | grep -vE "id:|sku:|resuelta:" | tr -d '"' | tr -d ',' | sed 's/^ *//' | grep "youtube:" | awk 'NF {print $NF}')"
        activeDirectory="$(cat bundle.js  | grep -i "activeDirectory: " -B 9 | grep -i "name: \"$name\"" | awk 'NF{print $NF}' | tr -d '"' | tr -d ',')"
        bufferOverflow="$(cat bundle.js  | grep -i "bufferOverFlow: " -B 9 | grep -i "name: \"$name\"" | awk 'NF{print $NF}' | tr -d '"' | tr -d ',')"

        # Print variables
        echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
        echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
        echo -e "\n${purpleColor} ${endColor} Listing the properties of the machine${purpleColor} $name ${endColor}:\n"
        echo -e "${purpleColor} ${endColor} Name:\t\t${blueColor} $name ${endColor}"
        echo -e "${purpleColor} ${endColor} IP:\t\t\t${blueColor} $ip ${endColor}"
        echo -e "${purpleColor} ${endColor} Operating System:\t${yellowColor} $so ${endColor}"
        echo -e "${purpleColor} ${endColor} Difficulty:\t\t${blueColor} $dificultad ${endColor}"
        echo -e "${purpleColor} ${endColor} Certification:\t${blueColor}$like ${endColor}"

        if [ "$bufferOverflow" == "$name" ]; then
                echo -e "${purpleColor} ${endColor} Buffer Overflow:\t${endColor}${greenColor} YES  ${endColor}"
        #else
            #echo -e "${purpleColor} ${endColor} Buffer Overflow:\t${endColor}${blueColor}  ${endColor}"
        fi

        if [ "$activeDirectory" == "$name" ]; then
                echo -e "${purpleColor} ${endColor} Active Directory:\t${endColor}${greenColor} YES  ${endColor}"
        else
            echo -e "${purpleColor} ${endColor} Active Directory:\t${endColor}${blueColor} NO  ${endColor}"
        fi

        echo -e "${purpleColor} ${endColor} YouTube:\t\t ${redColor} ${endColor} $youtube"
        echo -e "${purpleColor} ${endColor} Skills:\t\t${blueColor}$skills${endColor}"

    else
        echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 {endColor}"
        echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
        echo -e "\n${redColor}✘ ERROR ✘${endColor}  The machine provided ${blueColor}\"$1\"${endColor} does not exist!\n"
    fi
}

function searchIp(){
  ipAddress="$1"
  machineName=$(cat bundle.js | grep "ip: \"$1\"" -B 3 | grep "name: " | awk 'NF{print $NF}' | tr -d '"' | tr -d ',')
  if [ "$machineName" ]; then
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${purpleColor} ${endColor} The machine with IP${purpleColor} $ipAddress${endColor} is${blueColor} \"$machineName\" ${endColor}\n"
  else
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${redColor}✘ ERROR ✘${endColor}  The IP address provided ${blueColor}\"$1\"${endColor} does not match any machine.\n"
  fi
}

function searchYT(){
  machineName="$1"
  machineNameCheck=$(cat bundle.js | awk "BEGIN {IGNORECASE = 1} /name: \"$machineName\"/,/resuelta:/" | grep -vE "id:|sku:|resuelta" | tr -d '"' | tr -d ',' | sed 's/^ *//' |grep youtube | awk 'NF{print $NF}')
  if [ "$machineNameCheck" ]; then
    urlYT=$machineNameCheck
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${purpleColor} ${endColor} The YouTube URL of the resolution of the machine${blueColor} \"$machineName\"${endColor} is:\n"
    echo -e "${redColor} ${endColor} ${purpleColor}$urlYT${endColor}\n"
  else
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 {endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${redColor}✘ ERROR ✘${endColor}  The machine provided ${blueColor}\"$1\"${endColor} does not exist!\n"
  fi
}

function searchDiff(){
  difficulty="$1"
  difficultyCheck=$(cat bundle.js | grep -i "dificultad: \"$difficulty\"" -B 5 | grep "name: " | awk 'NF{print $NF}' | tr -d '"' | tr -d ',' | sort | column)
  totalMachines=$(cat bundle.js | grep -i "dificultad: \"$difficulty\"" -B 5 | grep "name: " | awk 'NF{print $NF}' | wc -l)
  if [ "$difficultyCheck" ]; then
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${purpleColor} ${endColor} The available machines with the difficulty${purpleColor} \"$difficulty\"${endColor} selected are:\n"
    echo -e "${blueColor}$difficultyCheck${endColor}\n"
    echo -e "${blueColor}Total machines: $totalMachines${endColor}\n"
  else
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${redColor}✘ ERROR ✘${endColor} The difficulty provided does not exist. The options are: ${blueColor}(Easy, Medium, Hard, Insane)${endColor}\n"
  fi
}

function getOS() {
  os="$1"
  osCheck=$(cat bundle.js | grep -i "so: \"$os\"" -B 5 | grep "name: " | awk 'NF{print $NF}' | tr -d '"' | tr -d ',' | sort | column)
  totalMachines=$(cat bundle.js | grep -i "so: \"$os\"" -B 5 | grep "name: " | awk 'NF{print $NF}' | wc -l)
  if [ "$osCheck" ]; then
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${purpleColor} ${endColor} The available machines with Operating System${purpleColor} \"$os\"${endColor} are:\n"
    echo -e "${blueColor}$osCheck${endColor}\n"
    echo -e "${blueColor}Total machines: $totalMachines${endColor}\n"
  else
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${redColor}✘ ERROR ✘${endColor} The Operating System does not exist in the DB. The options are: ${blueColor}(Windows, Linux)${endColor}\n"
  fi
}

function getSkill(){
  skill="$1"
  getSkill=$(cat bundle.js | grep -i "skills: " -B 6 | grep -i "$skill" -B 6 | grep "name: " | awk 'NF{print $NF}' | tr -d '"' | tr -d ',' | sort | column)
  totalMachines=$(cat bundle.js | grep -i "skills: " -B 6 | grep -i "$skill" -B 6 | grep "name: " | awk 'NF{print $NF}' | wc -l)
  if [ "$getSkill" ]; then
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${purpleColor} ${endColor} The machines with the Skill ${purpleColor}\"$skill\"${endColor} are:\n"
    echo -e "${blueColor}$getSkill${endColor}\n"
    echo -e "${blueColor}Total machines: $totalMachines${endColor}\n"
  else
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${redColor}✘ ERROR ✘${endColor} Skill not found.\n"
  fi
}

function getCertif(){
  certif="$1"
  getCertif=$(cat bundle.js  | grep -i "like: " -B 7 | grep -i "$certif" -B 7 | grep -i "name: " | awk 'NF{print $NF}' | tr -d '"' | tr -d ',' | sort | column)
  totalMachines=$(cat bundle.js  | grep -i "like: " -B 7 | grep -i "$certif" -B 7 | grep -i "name: " | awk 'NF{print $NF}'| wc -l)
  if [ "$getCertif" ]; then
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${purpleColor} ${endColor} The machines with certification ${purpleColor}\"$certif\"${endColor} are:\n"
    echo -e "${blueColor}$getCertif${endColor}\n"
    echo -e "${blueColor}Total machines: $totalMachines${endColor}\n"
  else
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${redColor}✘ ERROR ✘${endColor} The certification ${purpleColor}\"$certif\"${endColor} was not found.\n"
  fi
}

function getOSDifficulty(){
  difficulty="$1"
  os="$2"
  getOSDiff=$(cat bundle.js | grep "so: \"$os\"" -C 4 -i | grep "dificultad: \"$difficulty\"" -B 5 -i | grep "name: " | awk 'NF{print $NF}' | tr -d '"' | tr -d ',' | sort | column)
  totalMachines=$(cat bundle.js | grep "so: \"$os\"" -C 4 -i | grep "dificultad: \"$difficulty\"" -B 5 -i | grep "name: " | awk 'NF{print $NF}' | wc -l)
  if [ "$getOSDiff" ]; then
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${purpleColor} ${endColor} The machines with Operating System${purpleColor} \"$os\"${endColor} and difficulty${purpleColor} \"$difficulty\"${endColor} are:\n"
    echo -e "${blueColor}$getOSDiff${endColor}\n"
    echo -e "${blueColor}Total machines: $totalMachines${endColor}\n"
  else
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${redColor}✘ ERROR ✘${endColor} The Operating System and/or the difficulty do not exist.\n"
  fi
}

function getCertDifficulty(){
  certif="$1"
  difficulty="$2"
  getCertDiff=$(cat bundle.js | grep -e ".*$certif" -B 7 -i | grep "dificultad: \"$difficulty\"" -B 5 -i | grep "name: " | awk 'NF{print $NF}' | tr -d '"' | tr -d ',' | sort | column)
  totalMachines=$(cat bundle.js | grep -e ".*$certif" -B 7 -i | grep "dificultad: \"$difficulty\"" -B 5 -i | grep "name: " | awk 'NF{print $NF}' | wc -l)
  if [ "$getCertDiff" ]; then
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${purpleColor} ${endColor} The machines with Certification ${purpleColor} \"$certif\"${endColor} and difficulty${purpleColor} \"$difficulty\"${endColor} are:\n"
    echo -e "${blueColor}$getCertDiff${endColor}\n"
    echo -e "${blueColor}Total machines: $totalMachines${endColor}\n"
  else
    echo -e "\n${yellowColor}󰒋  HTB MACHINES  󰒋 ${endColor}"
    echo -e "${purpleColor}By: 4ndyMcFly${endColor}\n"
    echo -e "\n${redColor}✘ ERROR ✘${endColor} The Operating System and/or the difficulty do not exist.\n"
  fi
}

#Check if Database exists, if not, downloads it.

if [ -f bundle.js ]; then
    if grep -qE 'Fácil|Media|Difícil' bundle.js; then
        sed -i 's/Fácil/Easy/g' bundle.js
        sed -i 's/Media/Medium/g' bundle.js
        sed -i 's/Difícil/Hard/g' bundle.js
    fi
else
    helpPanel
    downloadDB
    exit 0
fi 

# Indicators
declare -i parameter_counter=0

# Flags
declare -i flag_difficulty=0
declare -i flag_os=0
#declare -i flag_skill=0
declare -i flag_certif=0

while getopts "m:ui:y:d:o:s:c:h" arg; do
  case $arg in
    m) machineName="$OPTARG"; ((parameter_counter++));;
    u) ((parameter_counter+=2));;
    i) ipAddress="$OPTARG"; ((parameter_counter+=3));;
    y) machineName="$OPTARG"; ((parameter_counter+=4));;
    d) difficulty="$OPTARG"; flag_difficulty=1; ((parameter_counter+=5));;
    o) os="$OPTARG"; flag_os=1; ((parameter_counter+=6));;
    s) skill="$OPTARG"; ((parameter_counter+=7));;
    c) certif="$OPTARG"; flag_certif=1; ((parameter_counter+=8));;
    h) ;;
    *) ;;
  esac
done

if [ $parameter_counter -eq 1 ]; then
  searchMachine "$machineName"
elif [ $parameter_counter -eq 2 ]; then
  updateFiles
elif [ $parameter_counter -eq 3 ]; then
  searchIp "$ipAddress"
elif [ $parameter_counter -eq 4 ]; then
  searchYT "$machineName"
elif [ $parameter_counter -eq 5 ]; then
  searchDiff "$difficulty"
elif [ $parameter_counter -eq 6 ]; then
  getOS "$os"
elif [ $parameter_counter -eq 7 ]; then
  getSkill "$skill"
elif [ $parameter_counter -eq 8 ]; then
  getCertif "$certif"
elif [ $flag_difficulty -eq 1 ] && [ $flag_os -eq 1 ]; then
  getOSDifficulty "$difficulty" "$os"
elif [ $flag_difficulty -eq 1 ] && [ $flag_certif -eq 1 ]; then
  getCertDifficulty "$certif" "$difficulty"
else
  helpPanel
fi

