# Image Thief 

### Install
    pip install imagethief
    
    -------------------------OR------------------------------------------------
    
    git clone https://github.com/imdhanush/ImageThief
    cd ImageThief
    python setup.py install

### Dependencies used 
- [Flask](https://github.com/pallets/flask)
- [Requests](https://github.com/psf/requests)

### Server Demo
```python
from ImageThief import Thief

app = Thief(name=__name__)


app.add_plan('/image','image') # Plan to get image file
app.add_plan('/audio','audio') # plan to get audio file

app.steal()

```

### Client Demo
```python
from requests import get
from ImageThief import Decoder as fileSaver

url = 'http://localhost:5000'

# url = 'http://192.168.43.151:5000'

plan = '/audio'

fileExtension = '.mp3'
filenameToBeFetched = 'sampa.mp3'
filenameToBeSavedLocally = 'some.mp3'

a = get(url + plan, headers={'Ext': fileExtension, 'filename': filenameToBeFetched}).json()

if a['message'] == 'OK':
    fileSaver(a['data'], filenameToBeSavedLocally, response=a)
    print('File Saved with name ' + filenameToBeSavedLocally)
else:
    print('Error')
