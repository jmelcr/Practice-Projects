```python
import numpy as np
import matplotlib.pyplot as plt
from matplotlib import style
import warnings
from collections import Counter
style.use('fivethirtyeight')

#k class is a list of lists (features). r is another class - so 2 classes and their features
dataset = {'k':[[1,2],[2,3],[3,1]], 'r':[[6,5],[7,7],[8,6]]}
new_features = [1,1]

[[plt.scatter(ii[0],ii[1],s=100,color=i) for ii in dataset[i]] for i in dataset]
plt.scatter(new_features[0], new_features[1], s=100) #s is size
plt.show()


def k_nearest_neighbors(data, predict, k=3):
    if len(data) >= k:
        warnings.warn('K is set to a value less than total voting groups!')

    distances = []
    for group in data:            # for each group/ class in the dataset
        for features in data[group]: #for each ii
            euclidean_distance = np.linalg.norm(np.array(features) - np.array(predict))
            distances.append([euclidean_distance, group]) #list of lists where the first item in the list is the distance and the second is the group
            #we only care about the distances because we need to rank them to know what are the top 3

    votes = [i[1] for i in sorted(distances)[:k]] #i[1] is the group. once we sorted them we only care about the distances to 'k'
    vote_result = Counter(votes).most_common(1)[0][0]
    return vote_result

result = k_nearest_neighbors(dataset, new_features)
print(result)

plt.scatter(new_features[0], new_features[1], s=100)

result = k_nearest_neighbors(dataset, new_features)
plt.scatter(new_features[0], new_features[1], s=100, color = result)
plt.show()
```
