# Nearest Earth Objects Machine Learning


Supervised Kaggle Dosyasının Linki: https://www.kaggle.com/code/melihak635442/melihneosupervisedml

Unsupervised Kaggle Dosyasının Linki: https://www.kaggle.com/code/melihak635442/melihneounsupervisedml

Nasa'nın Dünyaya yakın cisimleri tespit ettiği ve bunları kütlesi, yarıçapı, hızı, uzaklığı ve tehlikeli olup olmadığına göre ayırdığı bir veri seti kullandım.
Bu veriler ışığında Gözetimli Makinme Öğrenmesi olarak Logistic Regression algoritmasını kullanmaya karar verdim. Bu algoritmayı seçme sebebim elimdeki verilerin hepsinin pozitif korelasyona sahip olmamasıydı.
Gözetimsiz Makine Öğrenmesi olarak ise K-Means algoritmasını kullanmaya karar verdim. Bu algoritmayı seçmeden önce anomali tespiti yapan algoritmaları denedim ancak verilerimde pek anomali bulunmmuyordu. Belirli verileri sağlayan cisimler tehlikeli olarak sınıflanıyordu. Bu sebeple K-Means algoritmasını kullandım.

Verilerimi kullanıma hazır hale getirmek için Verisetindeki id, isim ve hangi yörüngede olduğu sütunlarını veri setinden drop() fonksiyonuyla sildim. Sonrasında verilerimde NaN değerler olduğunu fark ettim ve mentoruma danıştığımda Simple Imputer algoritmasını kullanabileceğimi belirtti. Simple Imputer algoritmasını ortalama (mean) metoduyla kullandım.

Sıra Logistic Regression algoritmamı uygulamaya geldi. Algoritmayı test_size = 0.2 ve random_state = 42 değerleriyle eğitip kullandım ve doğruluk oranını hesapladığımda 0.87 değerini aldım. 

![image](https://github.com/user-attachments/assets/b738e0af-0498-478f-9425-82994d7e7934)

Sadece bu oran yeterli olmayacağı için f1 score'unu da hesapladım
Bunun için DecisionTree algoritmasını daha küçük parçalara böldüm ve GridSearch algoritmasını kullandım. İlginç bir şekilde GridSearch ile baktığımda entropy ve gini kriterleriyle 13 ve 14 derinliklerinin skorda bir değişikliğe sebep olmadığını fark ettim.

![image](https://github.com/user-attachments/assets/ba28ce09-e6e5-4c5d-9282-47aa2be11e77) 

Sonrasında F1 Score'u hesapladım ve aslında algoritmamın tehlikesizleri ayırmakta iyi olmasına rağmen tehlikeli olanları ayırmakta çok da başarılı olmadığını gördüm.

![image](https://github.com/user-attachments/assets/698eda1e-aa3a-450b-8064-cb1b1bf0a48e)

Gözetimsiz Öğrenme kısmında da veri setini aynı şekilde temizleyip optimize ettiğim için bu kısmı atlıyorum.
K-Means algoritmasını kullanmak için öncelikle Elbow Metodu ile N küme sayısının kaç olması gerektiğini buluyorum ve ilginç bir şekilde 3 değerini alıyorum.

![image](https://github.com/user-attachments/assets/35cfb28f-0788-4413-a620-8016bb95f1bf)

Sonrasında modelimi veri setine uyguluyorum ve Silhouette Skoru ile Calinski-Harabasz indeksini hesaplıyorum. Burada da aynı şekilde n_clusters değişkenini 2, 3 ve 4 değerleriyle hesaplatıyorum ve 3 değerinde en yüksek skora erişiyorum.

![image](https://github.com/user-attachments/assets/dd31fbd5-9e8b-456d-9752-891907c3a1fa)

Araştırdığımda ise Silhouette skorunun 0 ile 0.5 değerleri arasında olması ortalama bir başarıya sahip olduğunu gösteriyormuş. 

Sonuç olarak kullandığım veri seti, Gözetimli Makine Öğrenmesi Algoritmasında daha başarılı oranlar elde etmişti fakat orada da tehlikeli olanları belirlemekteki doğruluğu yüksek değildi. Gözetimli ve Gözetimsiz algoritmalarda ortalama sonuçlar verdiğini söyleyebiliriz.
