n = 0
while (n > 4 or n < 1):
    n = int(input("정방행렬의 차수를 입력 하시오"))

matrix = []

for i in range(n):
    inp = input(f"{i+1}행의 값을 띄어쓰기로 구분하여 입력하시오: ")
    inp += " " 
    row = []
    tmpNum = "" 
    
    for char in inp:
        if char == " ": 
            if tmpNum != "": 
                row.append(int(tmpNum))
                tmpNum = ""
        else:
            tmpNum += char 
            
    matrix.append(row)

print(f"입력된 행렬: {matrix}")

def getM(matrix, i, j):
    #(i, j) 원소를 제외한 소행렬을 반환하는 함수
    M = []
    for r in range(len(matrix)):
        if r == i:
            continue
        newRow = []
        for c in range(len(matrix[r])):
            if c == j:
                continue
            newRow.append(matrix[r][c])
        M.append(newRow)
    return M

def getdetM(matrix):
    #행렬식을 계산하는 함수
    n = len(matrix)
    if n == 1:
        return matrix[0][0]
    if n == 2:
        return matrix[0][0] * matrix[1][1] - matrix[0][1] * matrix[1][0]
    det = 0
    for c in range(n):
        det += ((-1) ** c) * matrix[0][c] * getdetM(getM(matrix, 0, c))
    return det

def getInvDet(matrix):
    #행렬식을 이용해 역행렬을 계산하는 함수
    det = getdetM(matrix)
    if det == 0:
        return "역행렬이 존재하지 않음"
    n = len(matrix)
    if n == 1:
        return [[1 / det]]
    co = []
    for r in range(n):
        coRow = []
        for c in range(n):
            minor = getM(matrix, r, c)
            coRow.append(((-1) ** (r + c)) * getdetM(minor))
        co.append(coRow)
    adjugate = []
    for c in range(n):
        adjRow = []
        for r in range(n):
            adjRow.append(co[r][c]) 
        adjugate.append(adjRow)
    inverse = []
    for r in range(n):
        invRow = []
        for c in range(n):
            invRow.append(adjugate[r][c] / det)
        inverse.append(invRow)
    return inverse

invDet = getInvDet(matrix)
#print(f"행렬식으로 구한 역행렬: {invDet}")

def getInvGJ(matrix):
    # 가우스-조던 소거법을 이용해 역행렬을 계산하는 함수
    n = len(matrix)
    aug = []
    for i in range(n):
        newRow = []
        for c in range(n):
            newRow.append(matrix[i][c])
        for j in range(n):
            if i == j:
                newRow.append(1)
            else:
                newRow.append(0)
        aug.append(newRow)
    for i in range(n):
        pivRow = i
        while pivRow < n and aug[pivRow][i] == 0:
            pivRow += 1
        if pivRow == n:
            return "역행렬 없음"
        if i != pivRow:
            tmp = aug[i]
            aug[i] = aug[pivRow]
            aug[pivRow] = tmp
        pivVal = aug[i][i]
        for k in range(2 * n):
            aug[i][k] = aug[i][k] / pivVal
        for j in range(n):
            if i != j:
                factor = aug[j][i]
                for k in range(2 * n):
                    aug[j][k] = aug[j][k] - factor * aug[i][k]
    inverse = []
    for i in range(n):
        invRow = []
        for j in range(n, 2 * n):
            invRow.append(aug[i][j])
        inverse.append(invRow)
    return inverse

invGJ = getInvGJ(matrix)
#print(f"가우스-조던 소거법으로 구한 역행렬: {invGJ}")

'''print(f"\n행렬식으로 구한 역행렬: {invDet}")
print(f"가우스-조던 소거법으로 구한 역행렬: {invGJ}")
if type(invDet) == str and type(invGJ) == str:
    print("둘 다 역행렬 없음")
elif type(invDet) == str or type(invGJ) == str:
    print("하나만 역행렬 없음")
else:
    isSame = True
    for i in range(n):
        for j in range(n):
            diff = invDet[i][j] - invGJ[i][j]
            if diff < 0:
                diff = -diff
            if diff > 0.00001:
                isSame = False
                break
        if isSame == False:
            break
    if isSame == True:
        print("둘이 같음")
    else:
        print("둘이 다름")'''

def verifyInverse(matrix, inverse):
    # 원본 행렬과 역행렬의 곱을 계산하여 단위 행렬이 나오는지 확인하는 함수
    if type(inverse) == str:
        print("역행렬이 존재하지 않아 검증할 수 없습니다.")
        return
    n = len(matrix)
    result = []
    for i in range(n):
        row = []
        for j in range(n):
            val = 0
            for k in range(n):
                val += matrix[i][k] * inverse[k][j]
            row.append(val)
        result.append(row)
    isIdentity = True
    for i in range(n):
        for j in range(n):
            if i == j:
                diff = result[i][j] - 1
            else:
                diff = result[i][j] - 0
            if diff < 0:
                diff = -diff
            if diff > 0.00001:
                isIdentity = False
    if isIdentity == True:
        print("검증 완료")
    else:
        print("검증 실패")

'''print(f"역행렬: {invGJ}")
verifyInverse(matrix, invGJ)'''
