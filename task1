"""
Телефонная книга
"""
from csv import DictReader, DictWriter
from os.path import exists


class NameError:
    def __init__(self, txt):
        self.txt = txt


class PhoneError:
    def __init__(self, txt):
        self.txt = txt


class NameError:
    def __init__(self, txt):
        self.txt = txt


def get_user_data():
    flag = False
    while not flag:
        try:
            first_name = input('Введите имя пользователя: ')
            if len(first_name) < 2:
                raise NameError('Не валидная длина!')
            last_name = input('Введите фамилию пользователя: ')

            phone_number = int(input('Введите номер телефона пользователя: '))
            if len(str(phone_number)) < 11:
                raise PhoneError('Неверная длина номра телефона!')
            x = input("Закончить ввод? ")
            if x == 'Да':
                flag = True
        except ValueError:
            print('Вы вводите символы вместо цифр!')
            continue
        except NameError as err:
            print(err)
            continue
        except PhoneError as err:
            print(err)
            continue
    return first_name, last_name, phone_number


def create_file(file_name):
    with open(file_name, 'w', encoding="utf-8") as data:
        f_writer = DictWriter(data, fieldnames=['Имя', 'Фамилия', 'Телефон'])
        f_writer.writeheader()


def copy_file(file_name, new_file_name):
    list_1 = list(read_file(file_name))
    y = int(input(f"Выберите номер строки c 1 по {len(list_1)}: "))
    result = [list_1[y - 1]]
    with open(new_file_name, 'w', encoding="utf-8", newline='') as data:
        f_writer = DictWriter(data, fieldnames=['Имя', 'Фамилия', 'Телефон'])
        f_writer.writeheader()
        f_writer.writerows(result)


file_name = 'phone.csv'
new_file_name = 'phone1.csv'


def read_file(file_name):
    with open(file_name, encoding="utf-8") as data:
        f_reader = DictReader(data)
        return list(f_reader)


def write_file(file_name):
    user_data = get_user_data()
    res = read_file(file_name)
    for el in res:
        if el['Телефон'] == str(user_data[2]):
            print('Такой пользователь уже существует!')
            return
    obj = {'Имя': user_data[0], 'Фамилия': user_data[1], 'Телефон': user_data[2]}
    res.append(obj)
    with open(file_name, 'w', encoding="utf-8", newline='') as data:
        f_writer = DictWriter(data, fieldnames=['Имя', 'Фамилия', 'Телефон'])
        f_writer.writeheader()
        f_writer.writerows(res)


def main():
    while True:
        command = input('Введите команду: ')
        if command == 'q':
            break
        elif command == 'w':
            if not exists(file_name):
                create_file(file_name)
            write_file(file_name)
            print('Данные успешно записаны!')
        elif command == 'r':
            if not exists(file_name):
                print('Фаил не создан, создайте его!')
                continue
            print(read_file(file_name))
        elif command == 'n':
            copy_file(file_name, new_file_name)


main()
