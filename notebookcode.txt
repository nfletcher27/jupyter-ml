import pandas as pd
music_data = pd.read_csv('music.csv')
music_data

X = music_data.drop(columns = ['genre'])
y = music_data['genre']


# Takes music.csv, splits into two sets, and asks for a prediction using predict()
import pandas as pd
from sklearn.tree import DecisionTreeClassifier

music_data = pd.read_csv('music.csv')
X = music_data.drop(columns = ['genre'])
y = music_data['genre']

model = DecisionTreeClassifier()
model.fit(X, y)
predictions = model.predict([ [21, 1], [22, 0] ])
predictions

# Takes .csv file, and uses .metrics method which will train, test, and split our data
# using a comparison between predictions and our real data (y_test) we get an accuracy score between 0 - 1
import pandas as pd
from sklearn.tree import DecisionTreeClassifier
from sklearn.model_selection import train_test_split
from sklearn.metrics import accuracy_score

music_data = pd.read_csv('music.csv')
X = music_data.drop(columns = ['genre'])
y = music_data['genre']
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2)

model = DecisionTreeClassifier()
model.fit(X_train, y_train)
predictions = model.predict(X_test)

score = accuracy_score(y_test, predictions)
score

# note that 'from sklearn.externals import joblib' has deprecated, now use simple 'import joblib as jb'
import pandas as pd
from sklearn.tree import DecisionTreeClassifier
import joblib as jb

music_data = pd.read_csv('music.csv')
X = music_data.drop(columns=['genre'])
y = music_data['genre']

model = DecisionTreeClassifier()
model.fit(X, y)

joblib.dump(model, 'music-recommender.joblib')

# Now that we have created our music-recommender.joblib file which is in our project directory, we can load it onto any prediction parameter
# This is called persisting
model = joblib.load('music-recommender.joblib')
predictions = model.predict([[21, 1]])
predictions

# Now we utilize tree to create our data visualization
import pandas as pd
from sklearn.tree import DecisionTreeClassifier
from sklearn import tree

music_data = pd.read_csv('music.csv')
X = music_data.drop(columns=['genre'])
y = music_data['genre']

model = DecisionTreeClassifier()
model.fit(X, y)

tree.export_graphviz(model, out_file='music-recommender.dot',
                     feature_names=['age', 'gender'],
                     class_names=sorted(y.unique()),
                     label='all',
                     rounded=True,
                     filled=True)

# This will have created a music-recommender.dot file, we can now put this into a VSCode format
# Install Graphviz(dot) language support for VSCode
