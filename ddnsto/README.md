�õģ��Ұ���дһ�������� `README.md` ʾ���������� **DDNSTO HA Add-on** ��Ŀ������������׶��������ǰ�װ�����ú�ʹ��˵����

```markdown
# DDNSTO Home Assistant Add-on

![Panel Icon](https://img.icons8.com/material/48/000000/domain.png)

DDNSTO ��̬�����������񼯳ɣ������Զ����¹��� IP �� DDNSTO ƽ̨��֧�� Home Assistant ʹ�á�

---

## ?? �汾

**��ǰ�汾:** 3.5.0  
**���ݼܹ�:** `amd64`, `aarch64`  
**�����ַ:** `ghcr.io/wuwweizn/ddnsto:3.5.0`  

---

## ?? ����

- �Զ�ͬ������ IP �� DDNSTO  
- ֧�� Home Assistant �����ʺ͹���  
- ��ܹ�֧�֣�amd64 / aarch64  

---

## ?? ��װ

### ͨ�� GitHub �ֿⰲװ

1. �� Home Assistant UI �У����� **���� �� �������̵� �� ����Զ���ֿ�**  
2. �ֿ��ַ�  
```

[https://github.com/wuwweizn/wwzn-china](https://github.com/wuwweizn/wwzn-china)

````
3. ��� ����ӡ� ������ `ddnsto`����װ����  

### ����װ���߼���

ֱ���� HA Add-on ������ʹ�þ���
```yaml
image: "ghcr.io/wuwweizn/ddnsto:3.5.0"
````

---

## ?? ����

�� Add-on ����ҳ����д��

```yaml
token: "��� DDNSTO Token"
```

> `token` ������ DDNSTO ƽ̨��ȡ����Ȩ�룬���ڸ�������������

---

## ?? ʹ��˵��

1. ���� Add-on
2. Add-on ���Զ�ʹ�� `token` ���¹��� IP
3. ��ͨ�� Home Assistant ���鿴״̬

---

## ?? �߼�����

* ֧�� `host_network: true`����֤ IP ����׼ȷ
* ֧�ֺ�̨�������� (`boot: manual`)
* ���ͼ�� `mdi:application-variable`

---

## ?? ע������

* ȷ�� GHCR �����Ѵ��ڲ����Ͷ�ܹ� manifest
* HA �汾��֧�� `image` �ֶ���Զ�̾���

---

## ?? ����

* [GitHub �ֿ�](https://github.com/wuwweizn/wwzn-china)
* [DDNSTO �ٷ���վ](https://www.ddnsto.com/)

---


