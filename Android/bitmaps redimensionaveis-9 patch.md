# Bitmaps redimensionáveis - arquivos 9-pacth

<smal>fonte: https://developer.android.com/guide/topics/graphics/drawables#nine-patch </smal>

A *ferramenta Draw 9-patch* é um _editor WYSIWYG integrado ao Android Studio_ que permite criar imagens de bitmap automaticamente redimensionáveis.
Os bitmaps se adaptam ao conteúdo da view e ao tamanho da tela. Determinadas partes da imagem são dimensionadas no eixo horizontal e vertical,
de acordo com os indicadores delineados dentro da imagem.

Um gráfico NinePatchDrawable é uma imagem bitmap esticável que pode ser usada como plano de fundo de uma visualização. O Android redimensiona automaticamente o gráfico para acomodar o conteúdo da view. Um exemplo de uso de uma imagem NinePatch é o plano de fundo usado pelos botões padrão do Android. Os botões precisam ser esticados para acomodar strings de vários tamanhos. Um gráfico NinePatch é uma imagem PNG padrão que inclui uma borda extra de 1 pixel. Ele precisa ser salvo com a extensão 9.png no diretório res/drawable/ do projeto.

Use a borda para definir as áreas esticáveis e estáticas da imagem. Indique uma seção esticável desenhando uma ou mais linhas pretas com 1 pixel de largura nas partes esquerda e superior da borda (os outros pixels de borda devem ser totalmente transparentes ou brancos). Você poderá usar quantas seções esticáveis quiser. O tamanho relativo das seções esticáveis não muda. Assim, a seção mais extensa será sempre a maior.

Também é possível definir uma seção de drawable opcional da imagem (linhas de preenchimento) desenhando uma linha à direita e outra na parte inferior. Se um objeto View definir o gráfico NinePatch como plano de fundo e especificar o texto da visualização, ele se esticará para que todo o texto ocupe somente a área designada pelas linhas direita e inferior (se forem incluídas). Se as linhas de preenchimento não forem incluídas, o Android usará as linhas esquerda e superior para definir essa área do drawable.

Para esclarecer a diferença, as linhas esquerda e superior definem quais pixels da imagem podem ser replicados para esticar a imagem. As linhas inferior e direita definem a área relativa dentro da imagem que o conteúdo da visualização pode ocupar.

A ferramenta Draw 9-patch oferece uma maneira muito prática de criar suas imagens NinePatch por meio de um editor gráfico WYSIWYG. Ele também gerará alertas se a região que você definiu para a área esticável estiver em risco de produzir artefatos de desenho como resultado da replicação de pixels.

A amostra de XML de layout a seguir demonstra como adicionar um gráfico NinePatch a alguns botões. A imagem do NinePatch é salva em res/drawable/my_button_background.9.png.

    <Button android:id="@+id/tiny"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentTop="true"
            android:layout_centerInParent="true"
            android:text="Tiny"
            android:textSize="8sp"
            android:background="@drawable/my_button_background"/>

    <Button android:id="@+id/big"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_alignParentBottom="true"
            android:layout_centerInParent="true"
            android:text="Biiiiiiig text!"
            android:textSize="30sp"
            android:background="@drawable/my_button_background"/>

Observe que os atributos layout_width e layout_height são definidos como wrap_content para que o botão se encaixe perfeitamente ao redor do texto.

A Figura 2 mostra os dois botões renderizados a partir do XML e da imagem do NinePatch mostrada acima. Observe como a largura e a altura do botão variam de acordo com o texto, e a imagem de plano de fundo é esticada para acomodá-lo. 

<img src="https://github.com/shnonomura/diarioProgramacao/blob/master/imagem/Android/botao%20renderizado%20por%20meio%20de%20um%20recurso%20XML%20e%20de%20um%20grafico%20NinePatch.jpg" alt="de botões pequenos e de tamanho normal">

<small>_Figura 2: botões renderizados por meio de um recurso XML e de um gráfico NinePatch._</small>

# Drawables Personalizados

Quando você quiser criar alguns desenhos personalizados, estenda a classe Drawable (ou qualquer uma das subclasses relacionadas).

O método mais importante a ser implementado é draw(Canvas), porque ele disponibiliza o objeto Canvas necessário para oferecer suas instruções de desenho.

O código a seguir mostra uma subclasse simples de Drawable que desenha um círculo:

    public class MyDrawable extends Drawable {
        private final Paint redPaint;

        public MyDrawable() {
            // Set up color and text size
            redPaint = new Paint();
            redPaint.setARGB(255, 255, 0, 0);
        }

        @Override
        public void draw(Canvas canvas) {
            // Get the drawable's bounds
            int width = getBounds().width();
            int height = getBounds().height();
            float radius = Math.min(width, height) / 2;

            // Draw a red circle in the center
            canvas.drawCircle(width/2, height/2, radius, redPaint);
        }

        @Override
        public void setAlpha(int alpha) {
            // This method is required
        }

        @Override
        public void setColorFilter(ColorFilter colorFilter) {
            // This method is required
        }

        @Override
        public int getOpacity() {
            // Must be PixelFormat.UNKNOWN, TRANSLUCENT, TRANSPARENT, or OPAQUE
            return PixelFormat.OPAQUE;
        }
    }
    
Então, você poderá adicionar o drawable onde quiser. Por exemplo, a uma ImageView, como mostrado aqui:

    MyDrawable mydrawing = new MyDrawable();
    ImageView image = findViewById(R.id.imageView);
    image.setImageDrawable(mydrawing);
    image.setContentDescription(getResources().getString(R.string.my_image_desc));

No Android 7.0 (API nível 24) e versões posteriores, também é possível definir instâncias do drawable personalizado com XML
    