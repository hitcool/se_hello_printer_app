# Simple Flask App

<a href="https://www.statuscake.com" title="Website Uptime Monitoring"><img src="https://app.statuscake.com/button/index.php?Track=hcQCNlqAEc&Days=1&Design=1" /></a>

<a href="https://travis-ci.org/hitcool/se_hello_printer_app"><img src="https://travis-ci.org/hitcool/se_hello_printer_app.svg?branch=master"></a>


Aplikacja Dydaktyczna wyświetlająca imię i wiadomość w różnych formatach dla zajęć
o Continuous Integration, Continuous Delivery i Continuous Deployment.

- W projekcie wykorzystamy virtual environment, dla utworzenia hermetycznego środowisko dla aplikacji:

  ```
  # tworzymy hermetyczne środowisko dla bibliotek aplikacji:
  $ python3 -m venv .venv

  # aktywowanie hermetycznego środowiska
  $ source .venv/bin/activate
  $ make deps - instalacja srodowiska

  $ make lint - sprawdzenie wygladu kodu
  $ make test - odpalenie testow
  $ make run  - uruchomienie aplikacji
  $ -----------------------------------
  $ (W nowym terminalu sudo su i w tedy wykonać)
  $ make docker_build - zbudowanie pakietu dockera
  $ make docker_run - uruchomienie aplikacji jako doker (tez z sudo)
  $ --------gdy coś nie działa: zaczymać->usunąć-> uruchomić proces--------
  $ docker stop hello-world-printer-dev - zatrzymanie dockera
  $ docker rm hello-world-printer-dev - wywalenie dockera
  $ make docker_run

  # aleternatywnie zamiast make deps
  $ pip install -r requirements.txt
  $ pip install -r test_requirements.txt

  # zobacz
  $ pip list
  ```

  Sprawdź: [tutorial venv](https://docs.python.org/3/tutorial/venv.html) oraz [biblioteki flask](http://flask.pocoo.org).

- Uruchamianie applikacji:

  ```
  # jako zwykły program
  $ python main.py

  # albo:
  $ PYTHONPATH=. FLASK_APP=hello_world flask run
  ```

- Uruchamianie testów (see: http://doc.pytest.org/en/latest/capture.html):

  ```
  $ PYTHONPATH=. py.test
  $ PYTHONPATH=. py.test --verbose -s
  ```

- Kontynuując pracę z projektem, aktywowanie hermetycznego środowiska dla aplikacji py:

  ```
  # deaktywacja
  $ deactivate
  ```

  ```
  ...

  # aktywacja
  $ source .venv/bin/activate
  ```

- Integracja z TravisCI:

  ```
  # miejsce na twoje notatki
  ```
  ----------------------------------------

## Pomocnicze

-----------------------------------------

- Instalacja dockera: [dockerce howto](https://docs.docker.com/install/linux/docker-ce/ubuntu/)

  ```
  # W nowej konsoli sudo su uruchamiamy:
  $ make decker_build
  $ make docker_run
  # zweryfikuj, że docker jest uruchomiony
  $ docker ps
  # sprawdź czy aplikacje działa poprawnie
  $ curl 127.0.0.1:5000

  # Docker zazwyczaj nie restartujemy, kasujemy i uruchamiamy na nowo:
  # docker stop hello-world-printer-dev
  # docker rm hello-world-printer-dev
  # make docker_run

  # Przydatne komendy docker-a (pamiętamy o sudo):
  # możemy uruchomieć basha w naszym dockerze
  $ docker run -it hello-world-printer /bin/bash
  # uruchamiamy bash-a w działającym dockerze z naszą aplikcją:
  $ docker exec -it hello-world-printer-dev /bin/bash

  ```
## Centos

  ```
  $ yum remove docker \
        docker-common \
        container-selinux \
        docker-selinux \
        docker-engine

  $ yum install -y yum-utils

  $ yum-config-manager \
      --add-repo \
      https://download.docker.com/linux/centos/docker-ce.repo

  $ yum makecache fast
  $ yum install -y docker-ce
  $ systemctl start docker
  ```
