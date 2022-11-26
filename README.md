# Instalación de bspwm y de sxhkd
En este repositorio se encuentra los archivos de configuración y una guía de instalación del gestor de ventanas _bspwm_ desde la fuente.
## Dependencias
En mi caso, mi sistema es un Ubuntu y siguiendo la [wiki](https://github.com/baskerville/bspwm/wiki) del creador debemos instalar las siguientes dependencias.
```
sudo apt update
```
```
sudo apt install libxcb-xinerama0-dev libxcb-icccm4-dev libxcb-randr0-dev libxcb-util0-dev libxcb-ewmh-dev libxcb-keysyms1-dev libxcb-shape0-dev
```
## Instalación
Clonamos los repositorios oficiales.
```
git clone --depth=1 https://github.com/baskerville/bspwm.git $HOME/temp/bspwm
```
```
git clone --depth=1 https://github.com/baskerville/sxhkd.git $HOME/temp/sxhkd
```
Compilamos e instalamos.
```
cd $HOME/temp/bspwm && make && sudo make install
```
```
cd $HOME/temp/sxhkd && make && sudo make install
```

Ya podemos borrar los archivos de instalación:
```
rm -rf $HOME/temp
```

## Configuración
### bspwm y sxhkd
Por defecto,  _bspwm_ y _sxhkd_ tiene archivos de configuración base que se encuentra en el directorio `/usr/local/share/doc/bspwm/examples/bspwmrc`.
Copiamos estos archivos en el directorio `$HOME/.config` del usuario.
```
mkdir -p $HOME/.config/bspwm
```
```
cp /usr/local/share/doc/bspwm/examples/bspwmrc $HOME/.config/bspwm/
```
Concedemos permisos de ejecución al archivo `bspwmrc`.
```
chmod u+x ~/.config/bspwm/bspwmrc
```

### sxhkd
```
mkdir -p $HOME/.config/sxhkd
```
```
cp /usr/local/share/doc/bspwm/examples/sxhkdrc $HOME/.config/sxhkd/
```
### Lightdm
Mi máquina usa _Lightdm_ como gestor de inicio de sesiones.
Por defecto, cuando _bspwm_ se instala guarda su sesión en el directorio `/usr/local/share/sessions`. 
Si iniciaramos  _Lightdm_ este no reconocería la sesión de  _bspwm_ porque no se encuentra en el directorio `/usr/share/xsessions`. Por lo tanto, debemos cambiar la sesión del _bspwm_ de directorio.
```
cp /usr/local/share/sessions/bspwm /usr/share/xsessions
