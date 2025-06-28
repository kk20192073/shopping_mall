[import 'dartio';.txt](https://github.com/user-attachments/files/20960654/import.dartio.txt)[Uploimport 'dart:io';

void main() {
  Map<String, int> products = {
    '셔츠': 45000,
    '원피스': 30000,
    '반팔티': 35000,
    '반바지': 38000,
    '양말': 5000,
  };
  
  //상품명과 가격을 한쌍으로 저장하기 위해 Map 자료구조 사용
  //빠른조 조회 (0(1))와 명확한 키-값 구조를 위해 List 대신 사용
 

  Map<String, int> cart = {};
  
  // 사용자 장바구니에 담은 상품명 + 수량을 저장
  // cart['양말'] = 3 처럼 누적계산에 편리하다

  while (true) {
    print('\n[1] 상품 목록 보기 / [2] 장바구니에 담기 / [3] 장바구니에 담긴 상품의 총 가격 보기 / [4] 프로그램 종료');
    stdout.write('선택: ');
    String? choice = stdin.readLineSync();
    
    //사용자 메뉴를 번복적으로 보여주기 위한 무한 루프(while(true))
    //4번 선택 시 break로 종료
    //사용자 입력을 받아 메뉴 선택 및 상품 정보 입력에 활용
    //null 안정성을 위해 String?로 선언하고 null 체크 수행

    if (choice == '1') {
      print('\n상품 목록:');
      products.forEach((name, price) {
        print('$name / ${price}원');
      });
      // Map의 각 요소를 순회허며 상품명과 가격 출력
    } else if (choice == '2') {
      stdout.write('\n상품 이름을 입력해 주세요 !\n');
      String? itemName = stdin.readLineSync();

      if (!products.containsKey(itemName)) {
        print('상품이 존재하지 않습니다.');
        continue;
      }
      //유효한 상품명인지 먼저 확인
      //수량 입력시
      //int? quantity = int.tryParse(quantityStr ?? '');
      //숫자가 아닌 입력 -> 오류 방지 위해 tryParse 사용
      //수량이 0이하 -> 사용자 안내후 건너뛴다.

      stdout.write('상품 개수를 입력해 주세요 !\n');
      String? quantityStr = stdin.readLineSync();
      int? quantity = int.tryParse(quantityStr ?? '');

      if (quantity == null || quantity <= 0) {
        print(quantity == 0 ? '0개보다 많은 개수의 상품만 담을 수 있어요 !' : '입력값이 올바르지 않아요 !');
        continue;
      }

      cart[itemName!] = (cart[itemName] ?? 0) + quantity;
      //담긴 모든 상품을 순회하며 가격 * 수량을 누적
      //products[name]!:null 아님을 보장을 한다.
      //containsKey로 이미 검증하기 때문이다.
      print('장바구니에 상품이 담겼어요 !');
    } else if (choice == '3') {
      int total = 0;
      cart.forEach((name, qty) {
        total += products[name]! * qty;
      });
      print('\n장바구니에 ${total}원 어치를 담으셨네요 !');
    } else if (choice == '4') {
      print('\n이용해 주셔서 감사합니다 ~ 안녕히 가세요 !');
      break;
      // 프로그램 종료를 위한 break
    } else {
      print('올바른 메뉴를 선택해 주세요.');
    }
  }
}



ading import 'dartio';.txt…]()
