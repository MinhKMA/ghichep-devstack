# Devstack 

Devstack là một loạt các scripts được sử dụng để nhanh chóng tạo lên được một môi trường Openstack dựa trên các phiên bản từ nhánh master trên git. Nó được sử dụng tương tác như một môi trường phát triển và làm cơ sở cho nhiều thử nghiệm chức năng của OpenStack.

## Hướng dẫn sử dụng nhanh 

### Chuẩn bị môi trường:

Ở đây mình cài đặt all in one:

- OS: Ubuntu 16
- Cấu hình 
    + Ổ cứng 50GB
    + RAM 4GB

### Thêm user `stack`

- Tạo nhanh một user `stack`

    ``sudo useradd -s /bin/bash -d /opt/stack -m stack``

- Vì người dùng này sẽ thực hiện nhiều thay đổi cho hệ thống nên nó cần có quyền sudo 

    ```sh
    echo "stack ALL=(ALL) NOPASSWD: ALL" | sudo tee /etc/sudoers.d/stack
    sudo su - stack
    ```

### Download repo devstack 

```sh
git clone https://git.openstack.org/openstack-dev/devstack
cd devstack
```

### Tạo file local.conf 

- Ở đây mình tạo một file đơn giản nhất nên đã disable cinder 


```sh 
[[local|localrc]]
SERVICE_TOKEN=minhkma
ADMIN_PASSWORD=minhkma
DATABASE_PASSWORD=minhkma
RABBIT_PASSWORD=minhkma
SERVICE_PASSWORD=minhkma
LOGFILE=$DEST/logs/stack.sh.log
LOGDAYS=2


##########################

# Enable normally
disable_service tempest
disable_service c-api
disable_service c-vol
disable_service c-sch


# Enable Neutron
enable_service neutron
enable_service q-svc
enable_service q-agt
enable_service q-l3,q-meta,q-dhcp
```

- Các bạn có thể tham khảo các file local.conf ở thư mục trong repo 

### Bắt đầu cài đặt 

``./stack.sh``

Bây giờ chúng ta chỉ cần chờ cho đến khi hoàn tất cài đặt. 








