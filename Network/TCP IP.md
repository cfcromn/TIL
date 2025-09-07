# TCP/IP

TCP/IP 4계층은 TCP/IP 프로토콜 통신 과정에 초점을 맞추어, OSI 7계층을 좀 더 단순화 시킨 계층을 의미한다.

# TCP/IP 4계층 모델

## 4계층: 응용 계층 (Application Layer)

주요 프로토콜: HTTP, FTP, SMTP, DNS 등

주요역할: 사용자와 직접 통신하며 응용 서비스 제공

## 3계층: 전송 계층 (Transport Layer)

주요 프로토콜: TCP, UDP

주요 역할:신뢰성 있는 전송(TCP) 또는 빠른 전송(UDP) 담당

## 2계층: 인터넷 계층 (Internet Layer)

주요 프로토콜: IP, ICMP, ARP

주요 역할: IP 주소를 기반으로 패킷을 목적지까지 전달

## 1계층: 네트워크 인터페이스 계층 (Network Interface Layer) 또는 링크 계층 (Link Layer)

주요 프로토콜: 이더넷, Wi-Fi, ARP 등

주요 역할: 실제 물리적인 전송 담당 (MAC 주소 기반 통신)

# 계층 간 데이터 흐름

- 응용 계층: 데이터를 생성 →
- 전송 계층: TCP/UDP 헤더 추가 →
- 인터넷 계층: IP 헤더 추가 →
- 네트워크 인터페이스 계층: MAC 헤더 추가 후 실제 전송