# Procedure installation SNORT

## packages necessaires (sudo si necessaire)

apt install -y libdaq-dev libhwloc-dev libpcap-dev libssl-dev libhwloc-dev libdumbnet-dev liblzma-dev libpcre3-dev zlib1g-dev libluajit-5.1-dev libssl-dev libnghttp2-dev libtool bison flex cmake git autoconf build-essential gawk libcmocka-dev libunwind-dev uuid-dev libsafe-dev


## Installation DAQ (pré-requis SNORT)

git clone https://github.com/snort3/libdaq.git

cd libdaq
./bootstrap
./configure --prefix=/usr/local/lib/daq_s3

make install

## Passer en root si 'ldconfig' ne fonctionne pas

sudo ldconfig


# Building SNORT

git clone https://github.com/snort3/snort3.git

## Export de l'installation

export my_path=/path/to/snorty
mkdir -p $my_path
cd snort3
./configure_cmake.sh --prefix=$my_path 

## Modification de chemin par defaut de LibDAQ

./configure_cmake.sh --prefix=$my_path \
                       --with-daq-includes=/usr/local/lib/daq_s3/include/ \
                       --with-daq-libraries=/usr/local/lib/daq_s3/lib/

## Compilation et installation de SNORT

cd build
make -j $(nproc)
make install

# Enfin vérification des installations 

$my_path/bin/snort -V


## On obtient cette sortie :   

"
,,_     -*> Snort++ <*-
o"  )~   Version 3.2.2.0
  
"


## Vérif DAQ

$my_path/bin/snort --daq-list



