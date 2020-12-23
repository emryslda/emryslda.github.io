---
title: "Wetterzentrale TopKarten download"
categories: [Weather,Other]
header:
  og_image: /assets/images/og_image1.png
tags:
  - Bash
  - Java
  - Python
  - Jython
---


Simple bash scripts to download the wetterzentrale top karten of GFS and ECMWF for Europe
[Github repository][1]


In order to download the latest available pictures simply run:
{% highlight linenos %}
./dwetter -m GFS,ECM 
{% endhighlight %}

download the following codes:
<p></p>
the [*dwetter.sh*][2] file contains:
```bash
#/bin/bash

while test $# -gt 0; do
  case "$1" in
    -h|--help)
      echo "$Wetterzentrale images download"
      echo " "
      echo "$package [options] application [arguments]"
      echo " "
      echo "options:"
      echo "-h, --help                show brief help"
      echo "-m, --model=ECM(ECMWF),GFS,..      specify the model to download"
      echo "-d, --domain=DOM1,DOM2,...	      specify the domain of the model" 
      echo "-o, --output-dir=DIR      specify a directory to store output in"
      exit 0
      ;;
    -d)
      shift
      if test $# -gt 0; then
        export DOMAIN=$1
      else
        echo "no domain specified"
        exit 1
      fi
      ;;
    -m*)
      shift
      if test $# -gt 0; then
        export PROCESS=$1
	for i in $(echo $PROCESS | sed "s/,/ /g")
	do
        bash model.sh $i
    	# call your procedure/other scripts here below
    	echo "$i"
	done
      else
        echo "no model specified"
        exit 1
      fi
      shift
      ;;
    --model*)
      
      ;;
    -o)
      shift
      if test $# -gt 0; then
        export OUTPUT=$1
      else
        echo "no output dir specified"
        exit 1
      fi
      shift
      ;;
    --output-dir*)
      export OUTPUT=`echo $1 | sed -e 's/^[^=]*=//g'`
      shift
      ;;
    *)
      break
      ;;
  esac
done
```
<p></p>
the [*model.sh*][3] file contains:
```bash
#/bin/bash

WD="$(pwd)"
WD="${WD}/"
cd ${WD}
mkdir MAPS
WD="${WD}MAPS/"
model=$1
domain=1
echo $1

if [ $1 == GFS ]; then	
	nstep=3
	hour_int=( 00 06 12 18 )

elif [ $1 == ECM ]; then
	model=ECM
	nstep=24 #step of charts
        hour_int=( 00 12 )
fi
nfinal=144

cd ${WD}
rm -r ${model}
mkdir ${model}
cd ${model}

##################### END USER #################
for time in "${hour_int[@]}";
	do
        echo ${time}
	mkdir ${time}

	cd "${WD}${model}/${time}"

	for hour in `seq 0 ${nstep} ${nfinal}`
		do    
  		echo "Downloading hour..."$hour 
		url="www.wetterzentrale.de/maps/${model}OPEU${time}_${hour}_${domain}.png"
		echo ${url}
		wget ${url}
	done
	cd "${WD}${model}/"
done

cd "${WD}
```

[1]: https://github.com/emryslda/Wetterzentrale_TopKarten_download
[2]: https://github.com/emryslda/Wetterzentrale_TopKarten_download/blob/master/dwetter
[3]: https://github.com/emryslda/Wetterzentrale_TopKarten_download/blob/master/model.sh

<!-- Place this tag in your head or just before your close body tag. -->
<script async defer src="https://buttons.github.io/buttons.js"></script>
<!-- Place this tag where you want the button to render. -->
<!-- Place this tag where you want the button to render. -->
<a class="github-button" href="https://github.com/emryslda" data-color-scheme="no-preference: light; light: light; dark: dark;" data-size="large" aria-label="Follow @emryslda on GitHub">Follow @emryslda</a>

