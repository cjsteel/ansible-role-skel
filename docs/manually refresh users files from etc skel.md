Backup

```shell
TIMESTAMP=`date +"%Y-%m-%d--%T"`
echo $TIMESTAMP
#
cp $HOME/.bashrc $HOME/.bashrc-$TIMESTAMP
cp $HOME/.profile $HOME/.profile-$TIMESTAMP
cp $HOME/.bash_aliases $HOME/.bash_aliases-$TIMESTAMP
cp $HOME/.bash_logout $HOME/.bash_logout-$TIMESTAMP
cp -r $HOME/bin $HOME/bin-$TIMESTAMP
```

Delete originals

```shell
rm $HOME/.bashrc
rm $HOME/.profile
rm $HOME/.bash_aliases
rm $HOME/.bash_logout
rm -Rf $HOME/bin
```

Copy /etc/skel version

```shell
cp /etc/skel/.bashrc $HOME/.bashrc
cp /etc/skel/.profile $HOME/.profile
cp /etc/skel/.bash_aliases $HOME/.bash_aliases
cp /etc/skel/.bash_logout $HOME/.bash_logout
cp -r /etc/skel/bin $HOME/bin
```

