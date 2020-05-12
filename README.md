Giả sử bạn có 2 tasks bất đồng bộ trên 2 tiến trình riêng biệt, bạn muốn sau khi 2 tasks này được thực hiện xong thì thực hiện 1 tác vụ nào đó như hiển thị thông báo lên màn hình. Lúc này bạn có thể sử dụng Dispatch Group để thực hiện được điều đó. Dispatch Group sẽ chờ cho đến khi có tín hiệu thực hiện xong các tasks và sẽ thực hiện task tiếp theo.

 Ví dụ:

        let dispatchGroup = DispatchGroup()
        
        dispatchGroup.enter()
        taskOne { dispatchGroup.leave() }
        
        dispatchGroup.enter()
        taskTwo { dispatchGroup.leave() }
        
        dispatchGroup.notify(queue: .main) {
            print("Both tasks complete ")
        }

Khi số lượng hàm leave() được gọi bằng số lượng hàm enter(), hàm notify() sẽ được gọi.

Ngoài ra bạn có thể dùng hàm wait(timeout: ) thay cho hàm notify nếu bạn muốn chỉ định chờ trong một khoảng thời gian nhất định, nếu vượt quá thời gian đó mà vẫn chưa thực hiện xong các async tasks thì thực thi code trong hàm wait

