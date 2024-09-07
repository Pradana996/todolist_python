# todolist_python

import datetime

tasks = []

def add_task(title, description="", due_date=None):
    task = {
        "title": title,
        "description": description,
        "due_date": due_date,
        "status": "Belum Selesai"
    }
    tasks.append(task)
    print("Tugas baru berhasil ditambahkan!")

def view_tasks():
    if not tasks:
        print("Tidak ada tugas.")
        return

    print("Daftar Tugas:")
    for i, task in enumerate(tasks, start=1):
        print(f"{i}. {task['title']}")
        if task['description']:
            print(f"   Deskripsi: {task['description']}")
        if task['due_date']:
            print(f"   Jatuh Tempo: {task['due_date']}")
        print(f"   Status: {task['status']}")
        print()

def delete_task(task_index):
    if task_index < 1 or task_index > len(tasks):
        print("Indeks tugas tidak valid.")
        return
    
    deleted_task = tasks.pop(task_index - 1)
    print(f"Tugas '{deleted_task['title']}' berhasil dihapus.")

def mark_as_completed(task_index):
    if task_index < 1 or task_index > len(tasks):
        print("Indeks tugas tidak valid.")
        return
    
    tasks[task_index - 1]["status"] = "Selesai"
    print("Tugas berhasil ditandai sebagai selesai.")

while True:
    print("\nMenu:")
    print("1. Tambah Tugas")
    print("2. Lihat Tugas")
    print("3. Hapus Tugas")
    print("4. Tandai Tugas Sebagai Selesai")
    print("5. Keluar")

    choice = input("Pilih menu: ")

    if choice == '1':
        title = input("Masukkan judul tugas: ")
        description = input("Masukkan deskripsi (opsional): ")
        due_date_str = input("Masukkan tanggal jatuh tempo (YYYY-MM-DD, opsional): ")
        if due_date_str:
            due_date = datetime.datetime.strptime(due_date_str, "%Y-%m-%d").date()
        else:
            due_date = None
        add_task(title, description, due_date)
    elif choice == '2':
        view_tasks()
    elif choice == '3':
        task_index = int(input("Masukkan indeks tugas yang ingin dihapus: "))
        delete_task(task_index)
    elif choice == '4':
        task_index = int(input("Masukkan indeks tugas yang ingin ditandai sebagai selesai: "))
        mark_as_completed(task_index)
    elif choice == '5':
        break
    else:
        print("Pilihan tidak valid.")
