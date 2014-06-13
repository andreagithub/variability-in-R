variability-in-R


Velvet 
10/06/2014 

misure di variabilità 



Premessa:
Le misure di variabilità sono di importanza cruciale nell'analisi dei dati e quindi anche per Velvet Analytics.


creiamo un vettore di esempio che potrebbe essere il nostro dataframe di dati reali
y <- c(13,7,5,12,9,15,6,11,9,7,12) # creo un vettore di nome y (la nostra variabile di studio) 
								   # c sta per concatena i numeri all interno della parentesi (sono le nostre osservazioni delle variabili)
y # vedo il contenuto di y
# grafico 1
plot(y,ylim=c(0,20)) grafico dei valori contenuti in y
                     ylim serve per delimitare in ascissa la scala da 0 a 20
					 
# una prima misura della variabilità: il range					 
range(y) # il range (valora min e max) è la misura più semplice di variabilità
# grafico 2
plot(1:11,y,ylim=c(0,20),pch=16,col="blue") # lo stesso grafico sopra con pallini blue
lines(c(4.5,4.5),c(5,15),col="brown") # aggiungo una linea vertical marrone tipo di linea lty=1=continua
lines(c(4.5,3.5),c(5,5),col="brown",lty=2) # aggiungo linea verticale lty=2=tratteggiata = valore massimo
lines(c(4.5,5.5),c(15,15),col="brown",lty=2) # aggiungo linea verticale lty=2=tratteggiata = valore minimo

# quanto e come deviano le nostre osservazione dalla media
# grafico 3
plot(1:11,y,ylim=c(0,20),pch=16,col="blue")
abline(h=mean(y),col="green") # linea orizzontale che rappresenta la media dei dati

# plottiamo i residui = distanza di ogni punto dalla media
for (i in 1:11) lines(c(i,i),c(mean(y),y[i]),col="red") # disegna distanza di ogni osservazione dalla media = residui
# ma, la sommatoria delle distanze calcolate sopra è zero, meglio calcolare la somma dei quadrati
# infatti:
sum (y-mean(y))

# la somma dei quadrati:
# ecco perchè utilizziamo la somma dei quadrati:
sum((y - mean(y))^2) # abbiamo però il problema: è una misura di variabilità che dipende dalla grandezza del campione
                      cioè cresce all aumentare del campione

					 
# la deviazione quadratica media:
# meglio calcolare quindi la deviazione quadratica media 
# per fare questo ci calcoliamo i gradi di libertà:
# gradi di libertà di un campione n sono n-p, con p=numero di parametri da stimare dai nostri dati
# il nostro unico parametro da stimare dai dati per ora è la media quindi i gradi di libertà saranno: n-1 = 10
# la somma dei quadrati diviso i gradi di libertà è la varianza (varianza = sommadeiquadrati / gradidilibertà)

# la varianza:
sum((y-mean(y))^2)/(length(y)-1) 
# possiamo anche costruirci una funzione, che chiamiamo variance, per calcolarci la varianza:  
variance <- function (x)
sum((x-mean(x))^2)/(length(x)-1) 
variance(y)

# NB
# io non faccio mai tutti questi calcoli per calcolare la varianza...
# tutto questo lavoro in R si semplifica infatti con la seguente funzione built-in:
var(y)



# Morale
# La varianza è utilizzata in innumerevoli modi nell analisi statistica.
# Calcolarla non è una operazione semplice da fare manualmente: immagina calcolarla su un dataframe multivariato.
# Se riuscissimo ad integrare la funzione var() di R, sarebbe un successo garantito ed in breve tempo per Velvet.
