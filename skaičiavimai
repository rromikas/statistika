var imtisString = "-0.99	0.78	0.57	0.81	-0.59	-0.63	0.23	-1.88	-0.57	0.13 -1.38	-0.76	-0.11	-0.74	-1.70	-1.27	-0.24	0.31	0.96	-0.89 0.19	0.87	0.63	-0.08	-0.81	-0.99	-1.22	-1.67	0.87	-1.10 0.24	-0.06	-0.15	-0.81	0.63	-0.33	0.38	0.31	0.73	0.18 -1.99	-1.45	-1.26	-1.53	-1.06	-0.52	0.00	-1.97	-0.68	0.47 0.29	-0.44	0.56	-1.89	-0.36	-0.19	-0.75	0.50	-2.00	0.67 -1.13	-1.13	0.79	0.75	-0.39	-1.34	-0.37	-1.40	0.88	-1.96 0.45	0.70	0.78	-1.63	-1.11	-1.83	-0.29	0.90	-0.42	0.46 -0.29	-1.75	0.54	-1.72	-1.83	0.65	-0.37	-1.41	-0.65	0.08 -1.66	0.73	-1.35	-0.10	1.00	0.80	-0.80	0.96	-1.89	0.40";


var regex = /(-?)[0-9].[0-9]+/g;
var imtis = imtisString.match(regex);
console.log("Imtis: ", imtis);
var n = imtis.length;
console.log("n: " +  n);

imtis = imtis.map(x => {return parseFloat(x)});

var variacineEilute = imtis.sort((a, b) => {return a > b ? 1 : (a < b ? -1 : 0)})
console.log("Variacinė eilutė", variacineEilute);

var dazniai = {};

imtis.forEach(x => {
  if(!(x in dazniai))
  {
    dazniai[x] = 1;
  }

  else
  {
    dazniai[x]++;
  }
});

console.log("Imties dažniai", Object.keys(dazniai).map(x => {return x + ": " + dazniai[x]}));

var reducer = (accumulator, currentValue) => accumulator + currentValue;

var vidurkis = imtis.reduce(reducer) / imtis.length;

console.log("vidurkis", vidurkis);



PirmoKvartilioElementas = (n + (n % 2 === 0 ? 0 : 1)) * (1/4) - 1;
AntroKvartilioElementas = (n + (n % 2 === 0 ? 0 : 1)) * (3/4) - 1;
console.log("Kvartiliai", variacineEilute[PirmoKvartilioElementas], variacineEilute[AntroKvartilioElementas]);



var mediana = (variacineEilute[Math.floor(n/2) - 1] + variacineEilute[Math.floor(n/2 + 1) - 1]) / 2;

console.log("Mediana", mediana);

var maxDaznis = 0.0;
var moda;
Object.keys(dazniai).forEach(x => {
  if(dazniai[x] > maxDaznis)
  {
    moda = x;
  }
})

console.log("moda", moda)


var min = variacineEilute[0];
var max = variacineEilute[variacineEilute.length - 1];

console.log("Mažiausia reikšmė: ", min);

console.log("Didžiausia reikšmė", max);

var dispersija = imtis.reduce((acc, other) => acc + Math.pow(other - vidurkis, 2)) / n;

console.log("dispersija", dispersija);

var nuokrypis = Math.sqrt(dispersija);

console.log("standartinis nuokrypis", nuokrypis);

var k = Math.floor(1 + 3.22 * Math.log10(n));
console.log(k)

var to = Math.ceil(max);

var from = -Math.ceil(min / -1);
console.log(from, to)

var h = (to - from) / k;

var intervalai = {};

imtis.forEach(x => {
  var m = Math.floor(x / h);
  var f = m * h;
  var t = f + h;
  var path = "(" + f.toFixed(3).toString() + "; " + t.toFixed(3).toString() + ")";
  if(path in intervalai)
  {
    intervalai[path].daznis++;
  }

  else
  {
    var obj = {from: f, to: t, daznis: 1};
    intervalai[path] = obj;
  }
})

console.log("Intervalų dažniai", Object.keys(intervalai).map(x => { return x.toString() + " " + intervalai[x].daznis}));


var grVidurkis = Object.keys(intervalai).reduce((acc, other) => {return acc + ((intervalai[other].from + intervalai[other].to)/2*intervalai[other].daznis)}, 0) / n;

console.log("Grupuotų duomenų vidurkis: ", grVidurkis.toFixed(3));

var grDispersija = Object.keys(intervalai).reduce((acc, other) => {return acc + Math.pow((intervalai[other].from + intervalai[other].to)/2 - grVidurkis, 2)*intervalai[other].daznis}, 0) / (n - 1);

console.log("Grupuotų duomenų dispersija", grDispersija.toFixed(3));

var fun = ""

var acc = 0;

fun = fun + "       |" + acc + "    kai x <= " + intervalai[Object.keys(intervalai)[0]].from + ",\n";
Object.keys(intervalai).forEach((x, index) => {
  acc +=  intervalai[x].daznis / 100;

  if(index === 4)
  {
    fun += "F(x) = |" + acc + "    kai " + intervalai[x].from + " < x <= " + intervalai[x].to + ",\n";
  }
  else if(index === Object.keys(intervalai).length - 1)
  {
     fun = fun + "       |" + acc + "    kai " + intervalai[x].to + " < x,\n";
  }

  else
  {
    fun += "       |" + acc + "    kai " + intervalai[x].from + " < x <= " + intervalai[x].to + ",\n";
  }
  
  
})
//  fun = fun + "|" + acc + "    kai " + intervalai[Object.keys(intervalai).length - 1].to + " < x,\n";

console.log(fun);

var chi = Object.keys(intervalai).reduce((acc, other) => { return acc + (Math.pow((intervalai[other].daznis - n * (norm(intervalai[other].to) - norm(intervalai[other].from))), 2) / n * (norm(intervalai[other].to) - norm(intervalai[other].from)))}, 0)
console.log("chi kavadratas (jei hipoteze - normalusis)", chi);
console.log("Asdasda\nasdasdasd\nasdadsad")

function norm(x)
{
  return 1/(0.89*Math.sqrt(2*Math.PI)) * Math.pow(Math.E, (x + 0.4) / -1.6)
}

console.log(norm(-25))
