import gspread
from oauth2client.service_account import ServiceAccountCredentials

def search_user_by_national_code(sheet, national_code):

    rows = sheet.get_all_values()


    for row in rows:
        if row[0] == national_code:
            return row


    return None


def main():

    scope = ["https://spreadsheets.google.com/feeds", "https://www.googleapis.com/auth/drive"]
    creds = ServiceAccountCredentials.from_json_keyfile_name("credentials.json", scope)
    client = gspread.authorize(creds)

    sheet = client.open("نام Sheet شما").sheet1


    national_code = input("لطفاً کد ملی را وارد کنید: ")


    user_info = search_user_by_national_code(sheet, national_code)


    if user_info:
        print("مشخصات کاربر:")
        print(user_info)
    else:
        print("کاربری با این کد ملی یافت نشد.")


if __name__ == "__main__":
    main()
