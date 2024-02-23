<Div align="center">
    <div align="center" style="border: 1px solid #000; height:100%; width: 100%">
        <h1 align="center">⚙️ Dotfiles</h1>
    </div>
<p>📝 Instruções para personalização do Debian 12 com i3wm.</p>

<p>⚠️ O resultado final foi graças a configurações e tutoriais que eu achei online. Portanto, buscarei atribuir os devidos créditos, identificando cada autor com sua contribuição específica.</p>

<hr>
</div>
    <h1 align="center">Título</h1>
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

# Programas Necessários

xclip, maim, feh, picom, polybar