# Atividade em sala - HIRO

_Exexcícios feitos em sala_

### exemplo01.html

O exemplo 1 é apenas a aparição de um cubo (caixa) simples

```html
<body style="margin:0px; overflow:hidden;">
    <a-scene vr-mode-ui="enabled: false" arjs="debugUIEnabled:false">
        <a-marker present="hiro">
            <a-box color="#ff0e0e0e"></a-box>
        </a-marker>

        <a-entity camera="">

        </a-entity>
    </a-scene>
</body>
```

Cria-se uma cena dendro do Body, a qual faz a composição dos elementos, possuindo um marcador do cubo. Logo após temos a Entity que ativa a câmera

### exemplo02.html

No segundo exemplo, o cubo é substituído por uma imagem, nesse caso do Pikachu

```html
<body style="margin:0px; overflow:hidden;">
    <a-scene vr-mode-ui="enabled: false" arjs="debugUIEnabled:false">
        <a-assets>
            <img id="pikachu" src="./assets/025.png">
        </a-assets>

        <a-marker present="pikachu">
            <a-image width="1" height="1" rotation="-90 0 0" position="0 0 0" src="#pikachu"></a-image>
        </a-marker>

        <a-entity camera="">

        </a-entity>
    </a-scene>
</body>
```

Carregamos um asset da imagem e usamos no marcador no lugar do cubo

### exemplo03.html

Para o exemplo 3, a imagem acompanha também um áudio que ativa em simultâneo, no caso o som do Pikachu

```html
<body style="margin:0px; overflow:hidden;">
    <a-scene vr-mode-ui="enabled: false" arjs="debugUIEnabled:false">
        <a-assets>
            <audio id="som"  preload="auto" src="./assets/pokemon-pikachu-sound-effect-for-editing-128-ytshorts.savetube.me.mp3"></audio>
            <img id="hiro" src="./assets/025.png">
        </a-assets>

        <a-marker present="hiro">
            <a-image width="1" height="1" rotation="-90 0 0" position="0 0 0" src="#hiro"></a-image>
            <a-entity sound="src: #som; autoplay: true;"></a-entity>
        </a-marker>

        <a-entity camera="">

        </a-entity>
    </a-scene>
</body>
```

Além do asset da imagem, também inicamos um para o arquivo de áudio, esse que por sua vez é chamado jundo da imagem como uma Entity

### exemplo03-5.html

Dessa vez, no lugar de uma imagem e um áudio, é renderizado um vídeo já com áudio

```html
<a-scene vr-mode-ui="enabled: false" arjs="debugUIEnabled:false">
    <a-assets>  
        <video id="rick_rolled" src="./assets/Rick Astley - Never Gonna Give You Up.mp4" autoplay loop></video>
    </a-assets>

    <a-marker present="rick_rolled" controlador>
        <a-video width="1" height="1" rotation="-90 0 0" position="0 0 0" src="#rick_rolled"></a-video>
    </a-marker>

    <a-entity camera="">

    </a-entity>
</a-scene>
```

O vídeo é chamado como um asset e renderizado com o marcador específico para video. Além disso, nesse caso utilizamos uma tag de script para fazer com que o vídeo pare quando deixar de ser exibido na tela

```html
<script>
    // Aguardando a interação do usuário
    AFRAME.registerComponent(
        'controlador', {
            init: function(){
                this.toggle = false;
                this.vid=document.querySelector("#rick_rolled");
                this.vid.pause();
            },
            tick: function(){
                if (this.el.object3D.visible == true){
                    if(!this.toggle){
                        this.toggle = true;
                        this.vid.play();
                    }else{
                        this.toggle = false;
                        this.vid.pause();
                    }
                }
            }
        }
    );
    
</script>
```

### exemplo04.html

Para finalizar, o último exemplo utiliza um modelo em 3D do Mario (versão Mario64)

```html
<body style="margin:0px; overflow: hidden;">
    <a-scene vr-mode-ui="enabled: false" arjs="debugUIEnabled:false">
        <a-assets>
            <a-asset-item id="mario64" src="./assets/a_mario_64_model/scene.gltf"></a-asset-item>
        </a-assets>
        <a-marker present="hiro">
            <a-entity gltf-model="#mario64" rotation="-90 0 0" scale="10 10 10"></a-entity>
        </a-marker>
        <a-entity camera="">
        </a-entity>
    </a-scene>
</body>
```

O asset é carregado com a tag asset-item e chamado como uma Entity, parecido com a imagem do exemplo 2