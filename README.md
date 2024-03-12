# EnemyFirst
ランダムに動くウイルスオブジェクトのスクリプト。角度も設定できるよ。
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class EnemySpawner : MonoBehaviour
{
    private float speed;
    public float angle;

    public float duration = 5f; // オブジェクトが存在する時間
    public float minSpeed = 2f; // 最小速度
    public float maxSpeed = 5f; // 最大速度

    // Start is called before the first frame update
    void Start()
    {
        speed = Random.Range(minSpeed, maxSpeed); // スピードのランダム
        angle = Random.Range(0f, 180f); // 角度のランダム
    }

    // Update is called once per frame
    void Update()
    {
        // 角度をラジアンに変換
        float rad = angle * Mathf.Deg2Rad;

        // ラジアンから進行方向を設定
        Vector3 direction = new Vector3(Mathf.Cos(rad), Mathf.Sin(rad), 0);

        // 方向に速度を掛け合わせて移動ベクトルを求める
        Vector3 vec = direction * speed * Time.deltaTime;

        // 物体を移動する
        transform.position += vec;

        // 5秒後にオブジェクトを消す
        StartCoroutine(DestroyAfterDuration());
    }

    IEnumerator DestroyAfterDuration()
    {
        yield return new WaitForSeconds(duration);
        Destroy(gameObject);
    }
}
