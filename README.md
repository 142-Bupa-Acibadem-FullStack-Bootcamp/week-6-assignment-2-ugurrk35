# week-6-assignment-2

## Tic Tac Toe Uygulaması
![ezgif com-gif-maker (1)](https://user-images.githubusercontent.com/67828030/151440825-82b80609-991d-462d-94d2-6f7dcd7e5396.gif)

# Tic Tac Toe html /css /javascript ile yapımı


Tic-Tac-Toe JavaScript oyunu için HTML  
HTML ile başlamak. Bu, kodumuzun en basit ve kısa kısmıdır. Burada HTML öğelerimize sınıflar ve kimlikler atayacağız. Bu oyun içinde hücreler(cell) olan bir panodan(board) yapıldığı için hücreleri elementi ile oluşturacağız. Bu, daha sonra biçimlendireceğimiz genel kaplar oluşturacağımız anlamına gelir. Panomuz olabildiğince basit olacak.

oyun tahtası – Tic-Tac-Toe JavaScript oyunu

Muhtemelen zaten bildiğiniz gibi, bir tic-tac-toe oyunu 9 hücre (3×3) gerektirir. Dolu bir menü yerine, yeniden başlat butonu ile sona sadece bir mesaj ekleyeceğiz. HTML’mizin gövdesinde oluşturacağımız şey budur. HTML’miz şöyle görünecek:  

![](https://www.ugurkes.com/wp-content/uploads/2022/01/tic-tac-toe_04.png)

tic tac toe

```markup
<!DOCTYPE html>
<html lang="en">
<head>
 <meta charset="UTF-8">
 <meta http-equiv="X-UA-Compatible" content="IE=edge">
 <meta name="viewport" content="width=device-width, initial-scale=1.0">
 <link rel="stylesheet" href="style.css">
 <script src="script.js"></script>
 <title>Tic Tac Toe</title>
</head>
<body>

</body>
</html>
```

Head basit tutulur. Burada web sayfamızın başlığını belirledik ve index.html’yi stil sayfasına ve script dosyasına bağladık.  

## CSS – Style

Kodumuzun gelecek kısmı, hayal gücünüzü ve yaratıcılığınızı serbest bırakabileceğiniz yerdir. Stil sayfasında, oyunumuzun görsellerini kişiselleştirmek için kimlik etiketlerimizi ve sınıflarımızı kullanacağız. Kenarlıklar ve çizgi genişliğinden renklere ve metin boyutuna kadar. Kodun bu kısmı tamamen kişiselleştirilebildiğinden, kendi tercihlerinize uygun olarak sıfırdan yazabilir veya örneğimizi kullanabilirsiniz. Örneğimizi kullanacaksanız renkleri, boyutu, yazı tiplerini vb. de değiştirebilirsiniz.

```css
:root {
	--cell-size: 100px;

	--color: #81c3fd; /* for hover */
	--color-set: #0275d8; /* when set */
	--l: 10px; /* X line-width */
}
```

HTML’mizi görselleştirmekle başlayarak, kenar boşlukları tanımlanmış sınırlara sahip öğeler arasında boşluklar oluşturur, burada tüm ekran için sıfır kenarlık yapmak için kullanılır. Bundan sonra, genişliğini, yüksekliğini, nasıl ve nerede görüntüleneceğini belirterek öğeyi tahta sınıfımızın adıyla tanımlarız. grid-template-columns daha az bilinen bir özelliktir, bu yüzden basit tutmak için, bir grid düzenindeki sütunların sayısını ve genişliğinini belirtir. Bu şekilde 9 hücremizi oynamak için yapıyoruz.

```css
body {
	margin: 0;
}

.board {
	width: 100vw;
	height: 100vh;
	display: grid;
	justify-content: center;
	align-content: center;
	justify-items: center;
	align-items: center;
	grid-template-columns: repeat(3, auto)
}

```

Burada hücrelerimizin nasıl görünmesini istediğimizi belirtiyoruz. Genişlik ve yükseklik ile başlayarak, ardından kenarlıkların genişliği ve rengi, görüntü, konum ve imleç.

Sırada panomuzun daha çok bir Tic-Tac-Toe oyunu gibi göstermek. Dış hücrelerin tam bir kenarlığa sahip olmasını hariç tutuyoruz, böylece panomuz şöyle görünebilir:

![](https://www.ugurkes.com/wp-content/uploads/2022/01/tic-tac-toe_05-1024x416.png)

```css
/* remove border for edges */
.cell:nth-child(1), .cell:nth-child(2), .cell:nth-child(3) {
	border-top: none;
}

.cell:nth-child(1), .cell:nth-child(4), .cell:nth-child(7) {
	border-left: none;
}

.cell:nth-child(3), .cell:nth-child(6), .cell:nth-child(9) {
	border-right: none;
}

.cell:nth-child(7), .cell:nth-child(8), .cell:nth-child(9) {
	border-bottom: none;
}
```

Belirli bir hücre için kenarlık olmaması gerektiğini belirtiyoruz. O elemanı/hücreyi seçmek için hücrenin numarasını yazdığınız nth-child seçiciyi kullanarak bir hücre seçiyoruz.

```css
.cell.x, .cell.circle {
	cursor: not-allowed;
}
```

Burada, hücre zaten iki karakterimizden biriyle doluysa, fareyle üzerine gelme etkisinin olmadığını belirliyoruz.

### Oyuncu için bir çarpı işareti çizme

Bir çarpı çizmek biraz CSS büyüsü gerektirir. linear-gradient kullanarak renkleri bir kez daha beyaz, mavi (çapraz için) ve beyaz olarak 3 adımda tanımlarız. . Background settings biraz boşluk bırakmak ve çarpıyı ortalamak için.

```css
/* for cross */
.board.x .cell:not(.circle):not(.x):hover {
	background: linear-gradient(to top right, transparent calc(50% - var(--l) / 2), var(--color) calc(50% - var(--l) / 2) calc(50% + var(--l) / 2), transparent calc(50% + var(--l) / 2)),
				linear-gradient(to bottom right, transparent calc(50% - var(--l) / 2), var(--color) calc(50% - var(--l) / 2) calc(50% + var(--l) / 2), transparent calc(50% + var(--l) / 2));
	background-size: 80% 80%;
	background-repeat: no-repeat;
	background-position: center;
}
```

Renk için –color-set değişkenimizi kullanırız. Bunun için var işlevini kullandığımızı görebilirsiniz (var işlevi hakkında daha fazla bilgi edinin). Calc adında başka bir fonksiyon daha var(calc fonksiyonu hakkında bilgi edinin). Bu, her türlü ölçümü (px, pt, % gibi) aldığı ve bunları topladığı için özel bir fonksiyondur.

Hücrenin boş olması durumunda, üzerine gelme efekti renk için –color adlı bir değişken kullanır ve içine bir x veya o damgası koyarsak –color-set olur. Burada, o’nun gezinme etkisinin yanında x’i görebilirsiniz.

![](https://www.ugurkes.com/wp-content/uploads/2022/01/tic-tac-toe.png)

```css
/* for cross (set) */
.cell:not(.circle).x {
	background: linear-gradient(to top right, transparent calc(50% - var(--l) / 2), var(--color-set) calc(50% - var(--l) / 2) calc(50% + var(--l) / 2), transparent calc(50% + var(--l) / 2)),
				linear-gradient(to bottom right, transparent calc(50% - var(--l) / 2), var(--color-set) calc(50% - var(--l) / 2) calc(50% + var(--l) / 2), transparent calc(50% + var(--l) / 2));
	background-size: 80% 80%;
	background-repeat: no-repeat;
	background-position: center;
}
```

### Daire işareti çizme

Bir daire çizmek çok daha kolaydır, sadece bir satır alır. Ancak aynı prensip, sadece radial-gradient ile kullanılır.

```css
/* for circle */
.board.circle .cell:not(.circle):not(.x):hover {	
	background: radial-gradient(var(--color) 60%, transparent 60%);
}

/* for circle (set) */
.cell:not(.x).circle {
	background: radial-gradient(var(--color-set) 60%, transparent 60%);
}
```

## Tic-Tac-Toe script

Scriptimizin ilk birkaç satırında x ve o karakterlerimiz için sabit bir değişken oluşturuyoruz. Aşağıdaki tablo, oyunu kazanmak için hareket kombinasyonlarını sunar. Bu kombinasyonlar, kombinasyonlardan herhangi birinin mevcut oyunla eşleşip eşleşmediğini kontrol ederek oyunun bitip bitmediğini belirlememize yardımcı olacaktır.

```javascript
const PLAYER_X_CLASS = 'x'
const PLAYER_O_CLASS = 'circle'
const WINNING_COMBINATIONS = [
	[0, 1, 2],
	[3, 4, 5],
	[6, 7, 8],
	[0, 3, 6],
	[1, 4, 7],
	[2, 5, 8],
	[0, 4, 8],
	[2, 4, 6]
]
```

Burada, tüm pano öğelerinin, kazanan mesajın ve yeniden başlatma düğmesinin değerlerini kaydetmek için index.html’de atadığımız id etiketlerini kullandık. Bunun için getElementById() JavaScript yöntemini kullandık. Kazanan mesaj metni öğesi için, belirtilen seçiciyle eşleşen belge içindeki ilk öğeyi döndüren querySelector() yöntemini kullandık. Data-cell özniteliğini hedeflemek için köşeli parantezleri ([]) de kullandık.

```javascript
const cellElements = document.querySelectorAll('[data-cell]')
const boardElement = document.getElementById('board')
const winningMessageElement = document.getElementById('winningMessage')
const restartButton = document.getElementById('restartButton')
const winningMessageTextElement = document.getElementById('winningMessageText')
let isPlayer_O_Turn = false
```

Komut dosyasının bu bölümünde oyunu başlatmak için gameStart() adlı bir fonksiyon oluşturduk. isPlayer_O_Turn değişkenini false olarak ayarladık, yani ilk oynayan x karakteri olacak. İşlevin geri kalanı, önceki oyundan kalan tüm karakterleri kaldırır. Burada da fare tıklamaları olan board ‘ta olabilecek olayları tetikliyoruz.

```javascript
startGame()

restartButton.addEventListener('click', startGame)

function startGame() {
	isPlayer_O_Turn = false
	cellElements.forEach(cell => {
		cell.classList.remove(PLAYER_X_CLASS)
		cell.classList.remove(PLAYER_O_CLASS)
		cell.removeEventListener('click', handleCellClick)
		cell.addEventListener('click', handleCellClick, { once: true })
	})
	setBoardHoverClass()
	winningMessageElement.classList.remove('show')
}
```

HandleClick işlevinde, panodaki hücreler için fare tıklama olaylarını ele alıyoruz.. Kısacası, currentClass değişkeni, o anda sırası gelen (X veya O) karakterini kaydeder. Kazanan kombinasyonları oyunla karşılaştırarak birinin zaten kazanıp kazanmadığını kontrol etmek için if ifadesinde başka bir işlev kullanılır. Bu şekilde beraberlik olup olmadığı belirlenir.

```javascript
function handleCellClick(e) {
	const cell = e.target
	const currentClass = isPlayer_O_Turn ? PLAYER_O_CLASS : PLAYER_X_CLASS
	placeMark(cell, currentClass)
	if (checkWin(currentClass)) {
		endGame(false)
	} else if (isDraw()) {
		endGame(true)
	} else {
		swapTurns()
		setBoardHoverClass()
	}
}
```

gameEnd() işlevinden daha önce bahsedilmişti. Oyunu bitiren fonksiyondur. İşlev, hangi karakterin kazandığını belirten bir kazanan mesajı veya kazanan olmadığını belirten bir mesaj görüntüleyebilir – if ifadesinin sonucuna bağlı olarak bir beraberliktir.

```javascript
function endGame(draw) {
    if (draw) {
        winningMessageTextElement.innerText = "Draw!";
    } else {
        winningMessageTextElement.innerText = `${circleTurn ? "O's" : "X's"} Wins!`;
    }
    winningMessageElement.classList.add("show");
}
```

Daha önce bahsedilen bir diğer fonksiyon da isDraw() fonksiyonudur. Bu, bir beraberlik olması durumunda değeri döndürür; bu, oyuncuların hiçbirinin kazanmadığı anlamına gelir. Ayrıca, bir boole değeri döndürerek bir koşulu doğrulamak için bir dizinin tüm öğelerini kontrol eden isDraw işlevinde gizlenmiş olan güzel bir yöntem de vardır. Genellikle bir dizinin öğelerini test eden ve testi geçerlerse true (1) döndüren bir dizi olarak tanımlanır.

```javascript
function isDraw() {
	return [...cellElements].every(cell => {
		return cell.classList.contains(PLAYER_X_CLASS) || cell.classList.contains(PLAYER_O_CLASS)
	})
}
```

placeMark() ve swapTurns() iki kısa ve basit fonksiyondur. placeMark(), karakteri hücreye yerleştirir, currentClass, sıranın kimde olduğuna bağlı olarak ya bir X ya da bir O olur. İkinci işlev, karakter bir hücreye yerleştirildikten sonra dönüşleri değiştiren işlevdir.

```javascript
function placeMark(cell, currentClass) {
	cell.classList.add(currentClass)
}

function swapTurns() {
	isPlayer_O_Turn = !isPlayer_O_Turn
}
```

## Tic-Tac-Toe JavaScript oyununu daha etkileşimli hale getirme

JavaScript kodumuzun bir sonraki bölümünde, pano üzerinde imleç üzerinde gezinme efektini ayarlayacağız. Bu, oyuncunun hücreleri hedeflemesini kolaylaştıracaktır. Ayrıca oyunumuzu biraz daha duyarlı hale getiriyor.

```javascript
function setBoardHoverClass() {
	boardElement.classList.remove(PLAYER_X_CLASS)
	boardElement.classList.remove(PLAYER_O_CLASS)
	if (isPlayer_O_Turn) {
		boardElement.classList.add(PLAYER_O_CLASS)
	} else {
		boardElement.classList.add(PLAYER_X_CLASS)
	}
}
```

Hücreleri yerleştirmeden önce fare imlecimizle üzerlerinde gezinirken bir karakterin hücrelerde görünmesini istediğimizden, setBoardHoverClass() işlevi bunun etkileşimli kısmıyla ilgilenir. Etkileşimli öğeler, Tic-Tac-Toe JavaScript oyunumuzu daha ilginç hale getirecek.

```javascript
function checkWin(currentClass) {
	return WINNING_COMBINATIONS.some(combination => {
		return combination.every(index => {
			return cellElements[index].classList.contains(currentClass)
		})
	})
}
```

Ve son olarak JavaScript’imizin, panomuzda kazanan kombinasyonlardan herhangi biriyle eşleşip eşleşmediğini kontrol etmek için çağrılan checkWin() işlevi vardır.

### Oyun sonuçlarını görüntüleme

Css kodumuza birde bunları ekliyelim.

```css
.winning-message {
	display: none;
	position: fixed;
	top: 0;
	left: 0;
	right: 0;
	bottom: 0;
	background-color: var(--color-set);
	justify-content: center;
	align-items: center;
	color: white;
	font-size: 5rem;
	font-family: 'Courier New', Courier, monospace;
	flex-direction: column;
}
```

mesaj butonu ayarlıyalım

```css
.winning-message button {
	border-radius: 10px;
	font-size: 3rem;
	background-color: white;
	border: 1px solid var(--color-set);
	padding: .25em .5em;
	cursor: pointer;
}

.winning-message button:hover {
	background-color: var(--color-set);
	color: white;
	border-color: white;
}
```
###Güncelleme
Css dosyanında renk değişikleri yapıldı
