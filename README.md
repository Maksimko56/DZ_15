# Погружение в Python Д\З Семинара №15

## 
>### Напишите код, который запускается из командной строки и получает на вход путь до директории на ПК.
>### Соберите информацию о содержимом в виде объектов namedtuple.
>### Каждый объект хранит:
>>○ имя файла без расширения или название каталога,
>
>>○ расширение, если это файл,
>
>>○ флаг каталога,
>
>> ○ название родительского каталога.
>
>### В процессе сбора сохраните данные в текстовый файл используя логирование.

# Код: 
    from sys import argv
    import os
    import logging
    
    logging.basicConfig(filename="login.log", level="INFO", encoding="utf-8")
    
    
    def scan_folders(path_scan=None):
        if not path_scan:
            path_scan = os.getcwd()
        try:
            path_scan = argv[1]
        except IndexError:
            path_scan = path_scan
    
        try:
            os.chdir(path_scan)
        except FileNotFoundError as e:
            path_scan = os.getcwd()
            os.chdir(path_scan)
    
        for roots, dir, files in os.walk(os.getcwd()):
            file_name = dir
            extension = []
            root = roots.split("\\")[-1:]
            is_dir = True
            logging.info(f"{file_name=} {[extension]=} {[is_dir]=} {root=}")
            for file in files:
                is_dir = False
                *file_name, extension = file.split(".")
                logging.info(f"{file_name=} {[extension]=} {[is_dir]=} {root=}")
    
    
    if __name__ == '__main__':
        scan_folders()

