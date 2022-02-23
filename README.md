# docker1
Docker環境へのアップ                                                               

git clone https://github.com/sbs-kotani/docker1.git                                                              
git clone https://github.com/各自のgithub名/postingprj.git                                                              
python3 -m venv env                                                              
source env/bin/activate                                                              

cd docker1                                                              
docker-compose run django django-admin startproject postingprj .                                                               
sudo chown -R $USER:$USER .                                                              
cd ..                                                              
cp -r postingprj/media docker1/src                                                              
cp -r postingprj/postingapp docker1/src                                                              
cp -r -f postingprj/postingprj docker1/src                                                              
cp -r postingprj/static docker1/src                                                              
cp -r postingprj/templates docker1/src                                                              

cd docker1                                                              
nano src/postingprj/settings.py                                                              
              ALLOWED_HOSTS = ["*"]に変更                                                              

docker-compose run django python3 ./manage.py makemigrations                                                              
docker-compose run django python3 ./manage.py migrate                                                              
sudo chown -R $USER:$USER .                                                              

docker-compose up                                                              

以下のDB置換処理を行うとローカル環境で作成したデータを反映できる。                                                           
cd ..                                                           
cp -f postingprj/db.sqlite3 docker1/src/db.sqlite3                                                             
cd docker1                                                           
docker-compose up                                                              
