<Div align="center">
    <div align="center" style="border: 1px solid #0001; height:100%; width: 100%">
        <h1 align="center">⚙️ Dotfiles</h1>
    </div>
<p>📝 Instruções para personalização do Debian 12 com i3wm.</p>

<p>⚠️ O resultado final foi graças a configurações e tutoriais que eu achei online. Portanto, buscarei atribuir os devidos créditos, identificando cada autor com sua contribuição específica.</p>

<hr>
</div>
    <h2 align="center">🟡 Fontes</h1>
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
sudo apt install fonts-noto-cjk fonts-noto-color-emoji
```

O restante das fontes devem ser baixadas e instaladas manualmente:
1. Acesse o site: https://www.nerdfonts.com/
2. Baixe as fontes solicitadas
3. Crie uma pasta oculta na sua home :
    ```bash
    mkdir ~/.fonts
    ```
4. Mova as fontes extraídas para a pasta .fonts
5. Atualize o cache de fontes:
    ```bash
    fc-cache -fv
    ```

<div>
    <h2 align="center">🔴 Polybar</h2>
</div>

Essa é a aparência padrão da Polybar após a instalação:

![](https://raw.githubusercontent.com/polybar/polybar/master/doc/_static/default.png)

Primeiro faça a instalação padrão do [Polybar](https://github.com/polybar/polybar) e depois instale os [temas](https://github.com/adi1090x/polybar-themes)

Executar um tema:
```
.config/polybar/launch.sh --theme
```
substitua _**theme**_ pelo tema que você deseja aplicar.

Atualmente estou utilizando uma versão modificada do tema 'hacker'.
Caso queira utilizá-la, basta substituir a pasta 'hacker' deste repositório pela pasta padrão, localizada em: ~/.config/polybar.

Iniciar o Polybar junto com o sistema:

Edite o arquivo ~/.config/i3/config, e adicione o seguinte:
```
exec --no-startup-id exec .config/polybar/launch.sh --hack
```

# Programas Necessários

xclip, maim, feh, picom, polybar