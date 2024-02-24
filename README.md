<Div align="center">
    <div align="center" style="border: 1px solid #0001; height:100%; width: 100%">
        <h1 align="center">⚙️ Dotfiles</h1>
    </div>
<p>📝 Instruções para personalização do Debian 12 com i3wm.</p>

<p>⚠️ O resultado final foi graças a configurações e tutoriais que eu achei online. Portanto, buscarei atribuir os devidos créditos, identificando cada autor com sua contribuição específica.</p>

<hr>
</div>
    <h2 align="center">Fontes</h1>
</div>

Antes de prosseguir, é necessário instalar as seguintes fontes:
- Iosevka Nerd Font
- JetBrainsMono Nerd Font
- Symbols Nerd Font
- Noto Color Emoji
- Noto CJK (opcional)
 
>recomendo a instalação da fonte Noto CJK para a exibição de caracteres em outros idiomas como o coreano, por exemplo.

A instalação das fontes Noto Color Emoji e Noto CJK podem ser realizadas via terminal com o comando:

```
$ sudo apt install fonts-noto-cjk fonts-noto-color-emoji
```

O restante das fontes devem ser baixadas e instaladas manualmente:
1. Acesse o site: https://www.nerdfonts.com/
2. Baixe as fontes solicitadas
3. Crie uma pasta oculta na sua home :
    ```bash
    $ mkdir ~/.fonts
    ```
4. Mova as fontes extraídas para a pasta .fonts
5. Atualize o cache de fontes:
    ```bash
    $ fc-cache -fv
    ```


<div>
    <h2 align="center">Picom</h2>
</div>
Picom é um compositor leve criado para o Xorg.
Basicamente, o picom nos proporciona alguns efeitos como transparência, blur e sombras.

Instalação:
```
$ sudo apt install picom
```

Você pode criar algumas regras específicas com o picom. É possível, por exemplo, desabilitar o efeito de transparência em alguns programas específicos. Para ler mais, clique [aqui](https://wiki.archlinux.org/title/Picom).

Adicione a seguinte linha ao seu arquivo de configuração do i3 para que o picom seja inicializado junto com o sistema:
```
exec --no-startup-id picom
```
Não sei se funcionará no seu sitema como funcionou no meu, mas caso não esteja conseguindo colocar o efeito de blur, você pode optar por:
```
exec --no-startup-id picom --experimental-backends --blur-method box --blur-strength 3
```

<div>
    <h2 align="center">Polybar</h2>
</div>

Essa é a aparência padrão do Polybar:

![](https://raw.githubusercontent.com/polybar/polybar/master/doc/_static/default.png)

Primeiro faça a instalação padrão do [Polybar](https://github.com/polybar/polybar) e depois instale os [temas](https://github.com/adi1090x/polybar-themes)

Executar um tema:
```
$ .config/polybar/launch.sh --theme
```
substitua _**theme**_ pelo tema que você deseja aplicar.

Atualmente estou utilizando uma versão modificada do tema 'hacker'.
Caso queira utilizá-la, basta substituir a pasta 'hacker' deste repositório pela pasta padrão, localizada em: ~/.config/polybar.

Para iniciar o Polybar junto com o sistema, edite o arquivo ~/.config/i3/config, adicionando o seguinte:
```
exec --no-startup-id exec .config/polybar/launch.sh --hack
```

### Configurando o módulo mpd (Music Player Daemon):
Instale o mpd:
```
$ sudo apt install mpd
```
Crie uma pasta oculta dentro de home: 
```
mkdir ~/.mpd
```
Dentro dela, crie os seguintes arquivos: 
```
touch mpd.db mpd.pid mpd.log mpdstate
```
Crie e edite arquivo **mpd.conf**:
```
music_directory "~/Music/"
playlist_directory "~/Music/"
db_file "~/.mpd/mpd.db"
log_file "~/.mpd/mpd.log"
pid_file "~/.mpd/mpd.pid"
state_file "~/.mpd/mpdstate"
audio_output {
	type "pulse"
	name "pulse audio"
}
audio_output {
    type                    "fifo"
    name                    "my_fifo"
    path                    "/tmp/mpd.fifo"
    format                  "44100:16:2"
}
bind_to_address "127.0.0.1"
port "6601"
```
#### Opcionalmente, você pode instalar o **ncmpcpp**:
```
$ sudo apt install ncmpcpp
```
Crie uma pasta oculta dentro de home:
```
mkdir ~/.ncmpcpp
```
Dentro dela, crie e edite o arquivo **config**:
```
% egrep -v '^#' ~/.ncmpcpp/config
mpd_music_dir = "~/Music/"
visualizer_in_stereo = "yes"
visualizer_data_source = "/tmp/mpd.fifo"
visualizer_output_name = "my_fifo"
progressbar_look = "━━╸"
#visualizer_sync_interval = "30"

visualizer_type = "spectrum"
#visualizer_type = "wave"
#visualizer_type = "wave_filled"
#visualizer_type = "ellipse"

visualizer_look = "◆▋"
#visualizer_look = "+|"
#visualizer_look = "●●"

message_delay_time = "3"
playlist_shorten_total_times = "yes"
playlist_display_mode = "columns"
browser_display_mode = "columns"
search_engine_display_mode = "columns"
playlist_editor_display_mode = "columns"
autocenter_mode = "yes"
centered_cursor = "yes"
user_interface = "alternative"
follow_now_playing_lyrics = "yes"
locked_screen_width_part = "60"
display_bitrate = "yes"
external_editor = "nano"
use_console_editor = "yes"
header_window_color = "cyan"
volume_color = "red"
state_line_color = "yellow"
state_flags_color = "red"
progressbar_color = "yellow"
statusbar_color = "cyan"
visualizer_color = "cyan" #magenta #cyan #green #red #blue

mpd_host = "127.0.0.1"
mpd_port = "6601"
mouse_list_scroll_whole_page = "yes"
lines_scrolled = "1"
#ask_before_clearing_main_playlist = "yes"
enable_window_title = "yes"
song_columns_list_format = "(25)[cyan]{a} (40)[]{f} (30)[red]{b} (7f)[green]{l}"
```
Agora vamos inicializar e configurar pelo terminal:
```
$ mpd
```
```
$ systemctl start mpd
```
```
$ systemctl --user enable mpd.service
```
Pronto. Agora o mpd está configurado e pronto para ser exibido no polybar. Além disso, digitando [ncmpcpp](https://pkgbuild.com/~jelle/ncmpcpp/) no terminal, você tem acesso ao player de música.


<div>
    <h2 align="center">Rofi</h2>
</div>

O [rofi](https://github.com/davatorium/rofi) é uma alternativa ao dmenu, além de agregar algumas funções interessantes.

Primeiro, vamos instalar o programa:
```
$ sudo apt install rofi
```
Agora instale um pacote de funções extras com alguns temas insteressantes. Basta seguir o passo a passo em: https://github.com/adi1090x/rofi

Eu utilizo as funções de **launcher** e **powermenu**. Todos os temas são personalizáveis, basta se aventurar um pouco pelos arquivos de configuração. Caso não queira perder tempo, apenas copie a pasta 'rofi' deste repositório e substitua pela pasta padrão localizada em ~/.config

Adicionando atalhos de teclado no arquivo de configuração do i3:
```
bindsym $mod+Escape exec ~/.config/rofi/powermenu/type-4/powermenu.sh
bindsym $mod+d exec ~/.config/rofi/launchers/type-1/launcher.sh
```

Note que, nesse caso, o powermenu entrará em conflito com o [dmenu](https://wiki.archlinux.org/title/dmenu).

Eu resolvi isso alterando a keybind do dmenu:
```
bindsym $mod+Shift+d exec --no-startup-id dmenu_run
```

<div>
    <h2 align="center">Extras</h2>
</div>

#### Touchpad:
Edite o arquivo **/etc/X11/xorg.conf.d/90-touchpad.conf**:
```
Section "InputClass"
        Identifier "touchpad"
        MatchIsTouchpad "on"
        Driver "libinput"
        Option "Tapping" "on"
        Option "NaturalScrolling" "false"
        Option "TappingButtonMap" "lrm" # 1/2/3 finger, for 3-finger middle lrm
EndSection
```

#### Captura de tela:
```
$ sudo apt install maim xclip copyq
```

~/.config/i3/config:
```
##  Screenshots in files
bindsym Print exec --no-startup-id maim --format=png "/home/$USER/Pictures/screenshot-$(date -u +'%Y%m%d-%H%M%SZ')-all.png"
bindsym $mod+Print exec --no-startup-id maim --format=png --window $(xdotool getactivewindow) "/home/$USER/Pictures/screenshot-$(date -u +'%Y%m%d-%H%M%SZ')-current.png"
bindsym Shift+Print exec --no-startup-id maim --format=png --select "/home/$USER/Pictures/screenshot-$(date -u +'%Y%m%d-%H%M%SZ')-selected.png"

## Screenshots in clipboards
bindsym Ctrl+Print exec --no-startup-id maim --format=png | xclip -selection clipboard -t image/png
bindsym Ctrl+$mod+Print exec --no-startup-id maim --format=png --window $(xdotool getactivewindow) | xclip -selection clipboard -t image/png
bindsym Ctrl+Shift+Print exec --no-startup-id maim --format=png --select | xclip -selection clipboard -t image/png
```

#### Controle de brilho:
```
$ sudo apt install brightnessctl
```
~/.config/i3/config:
```
# brightnessctl control
bindsym XF86MonBrightnessUp exec --no-startup-id brightnessctl set 5%+

bindsym XF86MonBrightnessDown exec --no-startup-id brightnessctl set 5%-
```

#### i3lock manual mas personalizado:
```
$ sudo apt install scrot
```
~/.config/i3/config:
```
# lock screen with custom i3lock
bindsym $mod+Shift+Escape exec scrot -e 'convert $f -blur 4x4 $f && i3lock -i $f && rm $f'
```

#### Launcher de app (favoritos):
```
$ sudo apt install gnome-pie
```
Depois de instalado, basta adicionar os programas mais usados.

O atalho desse programa pode ser alterado diretamente nas suas configurações, não precisa especificar uma keybind no arquivo de configuração do i3.

#### Espaçamento e bordas coloridas
Edite da forma que achar melhor!

~/.config/i3/config:
```
# defining window borders

default_floating_border pixel 2
for_window [class="."] border pixel 2
for_window [class="^.*"] border pixel 2
gaps inner 18
#gaps outer 9

#  class                 border   bground  text    indicator  child_border
client.focused           #6eaa0e  #6eaa5e #FFFFFF  #6eaa5e     #a4dff4
client.focused_inactive  #333333  #5F676A #FFFFFF  #484E50     #000000
client.unfocused         #1iaa53  #222222 #888888  #292D2E     #000000

# remove gnome-pie borders
for_window [class="gnome-pie"] border pixel 0
```