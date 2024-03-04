import os
import csv
import datetime

def title():
    line_1 = ".............................."
    title = "contact management system"
    line_2 = ".............................."
    print(line_1.center(130))
    print(title.center(130))
    print(line_2.center(130))

class contact_functions:
    contact_fields = ["Name", "Mobile_No"]
    contact_database = "contacts.csv"

    def create(self):
        os.system('cls')
        title()
        print("create contacts:")
        print(".....................")
        print("")
        contact_data = []
        for field in self.contact_fields:
            contact_details = input("  Enter " + field + ": ")
            contact_data.append(contact_details)
        Date = datetime.datetime.today()
        d = Date.strftime("%d-%m-%Y")
        contact_data.append(d)
        with open(self.contact_database, 'a', newline='') as file:
            write = csv.writer(file)
            write.writerow(contact_data)
        print("")
        print("contact created successfully".center(128))
        print("\n")

    @staticmethod
    def view():
        os.system('cls')
        title()
        print("contacts".center(130))
        print(".....................")
        print("")
        count = 0
        with open(contact_functions.contact_database, 'r') as file:
            read = csv.reader(file)
            for data1 in read:
                if len(data1) > 0:
                    count += 1
                    print("total contacts:", count)
                    print('')
                    if os.path.getsize(contact_functions.contact_database) == 0:
                        print("contact book is empty, please create contacts".center(129))
                    else:
                        for field in contact_functions.contact_fields:
                            print('{0:<20}'.format(field), end="\t\t")
                        print('{0:<10}'.format("Date"))
                        print('{:<20}\t\t{:<10}'.format('............', '..........', '.......'))
                        print("")
                        file.seek(0)  # Reset file cursor
                        for data in read:
                            for item in data:
                                print('{:<20}'.format(item), end="\t\t")
                            print("\n")
                            input("\t press enter key to continue..".center(120))
                            os.system('cls')

    def search(self):
        os.system('cls')
        title()
        print("search contacts:")
        print(".............")
        print("")
        search_value = input("Enter contact name to search: ")
        found = False
        with open(self.contact_database, 'r') as file:
            read = csv.reader(file)
            for data in read:
                if len(data) > 3 and search_value == data[0]:
                    print('{:<20}\t\t{:<10}\t\t{:<10}'.format(data[0], data[1], data[2]))
                    found = True
        if not found:
            print("")
            print("Sorry, there is no contact with this name.".center(130))
            print("")
    def delete(self):
        os.system('cls')
        title()
        print("delete contacts:")
        print(".............")
        print("")
        contact_match = False  # Use boolean instead of string
        delete_value = input("Enter the name of the contact to delete: ")
        update_list = []
        with open(self.contact_database, 'r') as file:
            read = csv.reader(file)
            for data in read:
                if len(data) > 0:
                    if delete_value != data[0]:
                        update_list.append(data)
                    else:
                        contact_match = True  # Set contact_match to True if contact found
        if contact_match:
            with open(self.contact_database, 'w', newline='') as file:
                write = csv.writer(file)
                write.writerows(update_list)
            print("")
            print("Contact deleted successfully.".center(130))
            print("")
        else:
            print("")
            print("Sorry! Contact not found.".center(130))
            print("")
contact_class = contact_functions()
while True:
    print("1.view contacts".center(130))
    print("2.create contacts".center(130))
    print("3.search contacts".center(130))
    print("4.delete contacts".center(130))
    print("5.exit contacts".center(130))
    print("...................................".center(131))
    option = int(input("\t\t\t\t\t\tchoose your option:"))
    if option == 1:
        contact_class.view()
    elif option == 2:
        while True:
            contact_class.create()
            ans = input("\t\t\t\tDo you want to create another contact number?[Y/N]:")
            if ans.lower() != 'y':
                break
    elif option == 3:
        while True:
            contact_class.search()
            ans = input("\t\t\t\tDo you want to search another contact?[Y/N]: ")
            if ans.lower() != 'y':
                break
    elif option == 4:
        while True:
            contact_class.delete()
            ans = input("\t\t\t\tDo you want to create another contact number?[Y/N]:")
            if ans.lower() != 'y':
                break
    elif option == 5:
        os.system('cls')
        title()
        line_1="........................."
        msg   ="thank u for visiting our software"
        line_2="........................."
        print(line_1.center(130))
        print(msg.center(130))
        print(line_2.center(130))
        break
    else:
        print("Invalid option! Please choose a valid option.")
