# docker1
Docker環境へのアップ                                                               

sudo rm -rf 　docker1  env  postingprj　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　
git clone https://github.com/sbs-kotani/docker1.git                                                              
git clone https://github.com/各自のgithub名/postingprj.git                                                              
python3 -m venv env                                                              
source env/bin/activate                                                              

cd docker1 　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　
nano docker-compose.yml　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　
&nbsp;&nbsp;&nbsp;&nbsp;以下の箇所を変更する。Nは各自のSBS番号に変更する。　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　
　　container_name: nginx_sbsNpost　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　
　　………　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　
　　ports:　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　
　　- ‘700N:80’　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　
　　………　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　
　　container_name: django_sbsNpost　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　
　　………　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　
　　container_name: db_sbsNpost　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　　

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
