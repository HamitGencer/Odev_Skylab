import pandas as pd
import matplotlib.pyplot as plt

file_path = '/mnt/data/Housing.csv'
data = pd.read_csv(file_path)

data.info()
data.head()
plt.style.use('seagreen-firebrick')
fig, axes = plt.subplots(1, 3, figsize=(13, 6))

# Histogram 1:
axes[0].hist(data['area'], bins=13, color='dimgray', alpha=0.5)
axes[0].set_title('Ev Fiyatlarının Alanla İlişkisi')
axes[0].set_xlabel('Alan')
axes[0].set_ylabel('Ev Sayısı')

# Histogram 2: 
axes[1].hist(data['bedrooms'], bins=6, color='g', alpha=0.5)
axes[1].set_title('Ev Fiyatlarının Yatak Odası Sayısı ile İlişkisi')
axes[1].set_xlabel('Yatak Odası Sayısı (Bedrooms)')
axes[1].set_ylabel('Ev Sayısı')

# Histogram 3:
axes[2].hist(data['stories'], bins=6, color='darkcyan', alpha=0.5)
axes[2].set_title('Ev Fiyatlarının Kat Sayısıyla İlişkisi')
axes[2].set_xlabel('Kat Sayısı')
axes[2].set_ylabel('Ev Sayısı')
plt.tight_layout()
plt.show()

# 4. Ortalama fiyatlar:
bathroom_avg_price = data.groupby('bathrooms')['price'].mean()
furnishing_avg_price = data.groupby('furnishingstatus')['price'].mean()
fig, axes = plt.subplots(1, 2, figsize=(16, 6))

# Grafik 1: 
axes[0].bar(bathroom_avg_price.index, bathroom_avg_price.values, color='navy', alpha=0.5)
axes[0].set_title('Banyo Sayısına Göre Ortalama Ev Fiyatları')
axes[0].set_xlabel('Banyo Sayısı')
axes[0].set_ylabel('Ortalama Fiyat')

# Grafik 2: 
axes[1].bar(furnishing_avg_price.index, furnishing_avg_price.values, color='darkorange', alpha=0.5)
axes[1].set_title('Eşya Durumuna Göre Ortalama Ev Fiyatları')
axes[1].set_xlabel('Eşya Durumu')
axes[1].set_ylabel('Ortalama Fiyat')
plt.tight_layout()
plt.show()

# 5. Korelasyon Matrisi
correlation_matrix = data.corr()
plt.figure(figsize=(7, 6))
plt.matshow(correlation_matrix, cmap='olive', fignum=1)
plt.colorbar()
plt.title('Korelasyon Matrisi', pad=20)
plt.xticks(range(correlation_matrix.shape[1]), correlation_matrix.columns, rotation=90)
plt.yticks(range(correlation_matrix.shape[1]), correlation_matrix.columns)
plt.show()
print(correlation_matrix)
