---
title : "Giới thiệu"
date: 2025-07-01
weight : 1
chapter : false
pre : " <b> 1. </b> "
---




## Phiên bản DB
Phiên bản DB là môi trường cơ sở dữ liệu trên đám mây với các tài nguyên tính toán và lưu trữ mà bạn chỉ định.

Workshop **"AWS Cloud Deployment with Spring Boot and Docker"** hướng dẫn bạn cách triển khai một ứng dụng Spring Boot được đóng gói trong Docker image lên nền tảng Amazon Web Services (AWS), kết nối với cơ sở dữ liệu quan hệ (RDS) sử dụng MySQL. Mục đích của workshop này là trang bị cho bạn kiến thức thực tiễn về việc xây dựng, triển khai và quản lý ứng dụng Java trên đám mây, một kỹ năng quan trọng trong phát triển phần mềm hiện đại. Ứng dụng Spring Boot, nhờ sự tích hợp mạnh mẽ với Spring Data JPA và tính linh hoạt của Docker, cho phép triển khai nhanh chóng và mở rộng quy mô, trong khi AWS cung cấp hạ tầng đám mây đáng tin cậy với khả năng tự động hóa và bảo mật cao.

Workshop này được điều chỉnh từ tài liệu gốc "workshop aws-rds.txt", thay thế ứng dụng Node.js bằng Spring Boot và tích hợp với các biến môi trường tùy chỉnh (DBMS_*) hoặc chuẩn (SPRING_DATASOURCE_*) để kết nối database. Kết quả cuối cùng là một ứng dụng web hoạt động trên EC2, kết nối với RDS, và có thể được dọn dẹp dễ dàng sau khi hoàn thành. Nội dung phù hợp cho người mới bắt đầu với AWS cũng như các nhà phát triển muốn tối ưu hóa quy trình CI/CD (Continuous Integration/Continuous Deployment) bằng Docker và cloud computing. Sau workshop, bạn sẽ hiểu cách thiết lập cơ sở hạ tầng mạng (VPC), triển khai ứng dụng, và quản lý tài nguyên đám mây hiệu quả, áp dụng được trong các dự án thực tế như phát triển API, hệ thống quản lý người dùng, hoặc ứng dụng doanh nghiệp.

### Mục tiêu
- Triển khai ứng dụng Spring Boot từ Docker image trên Docker Hub lên Amazon EC2.
- Kết nối ứng dụng với cơ sở dữ liệu RDS MySQL (database first_cloud_users).
- Đảm bảo bảo mật, khả năng sẵn sàng cao (Multi-AZ), và quy trình dọn dẹp tài nguyên dễ dàng sau khi hoàn thành.

**Nội dung:**
- [Tạo Đám mây riêng ảo](#)
- [Tạo Mạng con trên nhiều Vùng khả dụng](#)
- [Tạo Nhóm bảo mật cho các phiên bản Amazon EC2](#v)
- [Tạo Nhóm bảo mật cho các phiên bản Amazon RDS DB](#)
- [Tạo Nhóm mạng con DB cho Amazon RDS](#)