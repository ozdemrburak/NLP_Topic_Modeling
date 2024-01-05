### PROJEDE EMEĞİ GEÇENLER

- Burak Özdemir 213405055
- Ömer Faruk Ak 213405004

# Haber Metinleriyle Konu Modelleme

Denetimsiz öğrenme algoritmalarını kullanarak metinlerin içerisindeki anlamsal bağları araştırıp sonucunda metinleri konulara göre ayrıştırır.

## KULLANILAN KÜTÜPHANELER

- Pandas
- Numpy
- Scikit-learn
- Nltk
- Pyplot
- re
- String
- Text_lemmatizer

# Veri Setinin Oluşturulması

Veri setini gazeteduvar.com.tr 'den requests BeatifulSoup kütüphaneleri kullanılarak oluşturulmuştur. Veri setini çektiğimiz site dinamik olmadığından Selenium kütüphanesine ihtiyaç duyulmamıştır.
![](https://github.com/ozdemrburak/NLP_Topic_Modeling/blob/main/project/images/burak5.jpg?raw=true)

- Görseldeki kodlarda 5 kategoriden 60957 url elde edilmiştir.
- 60457 url'den haber metinlerini aşağıdaki görseldeki kodlarla çekeceğiz.
  ![](https://github.com/ozdemrburak/NLP_Topic_Modeling/blob/main/project/images/burak1.png?raw=tru)
  > Kodda veri çektiğim sitenin html kodlarını inceleyerek elde ettiğim class bilgilerini kullanarak url'lerdeki tüm metinleri çektik. Daha sonra text_data listesi oluşturup for döngüsüyle metinleri listeye ekledik. Bu işlem çok uzun sürdüğü için 23326 adet url'den metin çekip veri seti oluşturma işlemini sonlandırdım. Ancak tüm url'lerden veri çekmediğimn için yalnızca 2 kategoriden (ekonomi-spor) haberlerini elde etmiş olduk.
  >
  > - Veri seti dengelidir. Yarı yarıya spor ve ekonomi haberleri içermektedir.
  > - Son olarak text_data listemizi önce df = pd.DataFrame(text_data) koduyla pandas dataframe'ine daha sonra da df.to_csv("dataset_turkce_haberler.csv") koduyla csv dosyasına çevirdik.
  >
  > * Dipnot: from IPython.display import clear_output kütüphanesiyle, veri çekerken kaçıncı iterasyonda olduğunu anlık olarak takip ettim.(bkz. görseldeki counter outputu )

# Modelin Eğitilmesi

## Metinlerin temizlenmesi

- > Veri seti oluşturulduktan sonra, modelin daha etkili çalışabilmesi ve başarı oranının artırılabilmesi için tweetlerin düzenlenmesi gerekmektedir. Bu düzenleme sürecinde, noktalama işaretleri, stopwords'ler, linkler gibi istenmeyen veriler tweetlerden temizlenir. Ardından, lemmatizasyon işlemi uygulanarak kelimelerin kökleri alınır ve temizlenmiş, kök kelimelerden oluşan tweetler elde edilir. Bu şekilde, modelin daha net ve anlamlı bir veri seti üzerinde eğitilmesi sağlanır, bu da başarı oranını artırabilir.
  > ![](https://github.com/ozdemrburak/NLP_Topic_Modeling/blob/main/project/images/burak2.png?raw=true)
- Görselde metin temizleme fonksiyonunu ve temizlenmiş bir metni görüyoruz. Metin temizleme işlemimiz başarılı gibi gözükmektedir.

# Modelin Oluşturulması

- Projede LDA ve NMF yöntemlerini kullanarak konu modelleme yapılmıştır. Sözcükleri vektörleştirmek için TF-IDF vectorizer kullanılmıştır.

![](https://github.com/ozdemrburak/NLP_Topic_Modeling/blob/main/project/images/burak3.png?raw=true)

> - Görselde LDA yöntemiyle elde ettiğimiz sonuçlara bakarsak Topic 3,4,6,7'de spor kategorisini, Topic 1,2,5,8' de ise ekonomi kategorisini modellediğini net bir şekikde görebiliriz.

![](https://github.com/ozdemrburak/NLP_Topic_Modeling/blob/main/project/images/burak4.png?raw=true)

> - Görselde LDA yöntemiyle elde ettiğimiz sonuçlara bakarsak Topic 2,3,5'de spor kategorisini, Topic 4,6,7,8' de ise ekonomi kategorisini modellediğini görebiliriz. Topic 1 içinse yorum yapmamız zor.

# Modellerin karşılaştırılması

> - LDA modelimizde topiclere baktığımızda alt başlıkları NMF'ye kıyasla net bir şekilde görebiliyoruz. Örneğin Topic 8'de ekonominin otomobil alt başlığını oluşturmuş. NMF'ye bakarsak topicler arasındaki fark çok da bariz değil. Aynı sözcükler birden fazla topicte geçiyor. Sonuç olarak 2 modeli de başarılı olarak değerlendirebiliriz ve LDA'nın NMF'den daha başarılı olduğunu söyleyebiliriz.
