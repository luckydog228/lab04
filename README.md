# lab04


## Задание

Вы продолжаете проходить стажировку в "Formatter Inc." (см подробности).



В прошлый раз ваше задание заключалось в настройке автоматизированной системы CMake.



Сейчас вам требуется настроить систему непрерывной интеграции для библиотек и приложений, с которыми вы работали в прошлый раз. Настройте сборочные процедуры на различных платформах:



используйте TravisCI для сборки на операционной системе Linux с использованием компиляторов gcc и clang;

используйте AppVeyor для сборки на операционной системе Windows.



для обоих случаев используем .github/actions



клонируем репозиторий предыдущей лабораторной



```

$ git clone https://github.com/luckydog228/lab03

```



создаём директорию workflows 



```

$ mkdir .github

$ cd ~/lab04/.github

$ mkdir workflows

$ cd ~/lab04/.github/workflows

```



Создаём файл Linux.yml



```

name: CMake



on:

 push:

  branches: [main]

 pull_request:

  branches: [main]



jobs: 

 build_Linux:



  runs-on: ubuntu-latest



  steps:

  - uses: actions/checkout@v3



  - name: Configure Solver

    run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build



  - name: Build Solver

    run: cmake --build ${{github.workspace}}/solver_application/build



  - name: Configure HelloWorld

    run: cmake -S ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build



  - name: Build HelloWorld

    run: cmake --build ${{github.workspace}}/hello_world_application/build

```


![VirtualBox_kali-linux-2023 1-virtualbox-amd64_30_05_2023_17_47_20](https://github.com/luckydog228/lab04/assets/128289395/34b0d1be-6970-452e-a3c8-5532dc34b837)



Создаём файл Windows.yml



```

name: CMake



on:

 push:

  branches: [main]

 pull_request:

  branches: [main]



jobs: 

 build_Windows:

  runs-on: windows-latest

  steps:

  - uses: actions/checkout@v3



  - name: Configure Solver

    run: cmake ${{github.workspace}}/solver_application/ -B ${{github.workspace}}/solver_application/build



  - name: Build Solver

    run: cmake --build ${{github.workspace}}/solver_application/build

    

  - name: Configure HelloWorld

    run: cmake -S ${{github.workspace}}/hello_world_application/ -B ${{github.workspace}}/hello_world_application/build



  - name: Build HelloWorld

    run: cmake --build ${{github.workspace}}/hello_world_application/build

```


![VirtualBox_kali-linux-2023 1-virtualbox-amd64_30_05_2023_17_48_26](https://github.com/luckydog228/lab04/assets/128289395/8e1f3961-b868-43dc-bf93-3b290d1dc80f)


```

$ git add .github

$ git commit -m "workflows"

$ git push origin main

```





Проверяем .github/actions

![VirtualBox_kali-linux-2023 1-virtualbox-amd64_30_05_2023_18_00_27](https://github.com/luckydog228/lab04/assets/128289395/9f758203-ef30-489a-a3fc-b0af2c1e9ad0)
![VirtualBox_kali-linux-2023 1-virtualbox-amd64_30_05_2023_18_00_41](https://github.com/luckydog228/lab04/assets/128289395/8fa6f0b5-e88f-478d-b360-73fc842cb6d8)
![VirtualBox_kali-linux-2023 1-virtualbox-amd64_30_05_2023_18_01_15](https://github.com/luckydog228/lab04/assets/128289395/9b0e8ccd-6050-4f8e-8e35-37f11f84f72c)



