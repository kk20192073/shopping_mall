import 'dart:io';

void main() {
  Map<String, int> products = {
    '셔츠': 45000,
    '원피스': 30000,
    '반팔티': 35000,
    '반바지': 38000,
    '양말': 5000,
  };

  Map<String, int> cart = {};

  while (true) {
    print('\n[1] 상품 목록 보기 / [2] 장바구니에 담기 / [3] 장바구니에 담긴 상품의 총 가격 보기 / [4] 프로그램 종료');
    stdout.write('선택: ');
    String? choice = stdin.readLineSync();

    if (choice == '1') {
      print('\n상품 목록:');
      products.forEach((name, price) {
        print('$name / ${price}원');
      });
    } else if (choice == '2') {
      stdout.write('\n상품 이름을 입력해 주세요 !\n');
      String? itemName = stdin.readLineSync();

      if (!products.containsKey(itemName)) {
        print('상품이 존재하지 않습니다.');
        continue;
      }

      stdout.write('상품 개수를 입력해 주세요 !\n');
      String? quantityStr = stdin.readLineSync();
      int? quantity = int.tryParse(quantityStr ?? '');

      if (quantity == null || quantity <= 0) {
        print(quantity == 0 ? '0개보다 많은 개수의 상품만 담을 수 있어요 !' : '입력값이 올바르지 않아요 !');
        continue;
      }

      cart[itemName!] = (cart[itemName] ?? 0) + quantity;
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
    } else {
      print('올바른 메뉴를 선택해 주세요.');
    }
  }
}
