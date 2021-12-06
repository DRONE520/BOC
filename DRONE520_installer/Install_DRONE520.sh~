echo "\033[37;1;45m Checking for the existepence of a local repository \033[0m"
cd ../
if (ls | grep -q PixHawk4 );
then {
       echo "PixHawk4 repo already cloned to $(pwd). What do you want to do?\n\t1)clone - delete local repo and clone new one \n\t2)pull - refresh repo using 'git pull'\n\t3)skip - do nothing"
       echo "Please specify proper action: "
       read answer
       case "$answer" in
       pull) {
       cd PixHawk4
       git pull
       cd ../
       };;
       clone) {
       rm -rf PixHawk4
       git clone https://github.com/DRONE520/PixHawk4 --recursive
       };;
       skip) {
       break
       };;
       *) {
       echo "Undefined option"
       };;
       esac
}
else {
git clone https://github.com/DRONE520/PixHawk4 --recursive
}
fi

echo "\033[37;1;45m Copying folder with custom scripts to repository \033[0m"

cp -a ./Install_DRONE520/DRONE520_modules ./PixHawk4/src/examples/
echo "***Folder copied to repo***"
if (cat./PixHawk4/boards/px4/sitl/default.cmake | grep app_ready > /dev/null);
then {
      echo "***Custom modules already added to defaul.cmake**"
      }
else {
sed -i 's/EXAMPLES/EXAMPLES\n\t\tpx4_simple_app_ready\' ./PixHawk4/boards/px4/sitl/default.cmake
echo "***Custom module added to defaul.cmake**"
}
fi
echo "Do you want to build sitl-simulation? (y/n)"
read answer
case "$answer" in
y) {
cd PixHawk4
make px4_sitl jmavsim
};;
n) break;;
*) {
echo "Undefined option"
break
};;
esac
