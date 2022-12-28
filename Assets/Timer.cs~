using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using UnityEngine.UI;
using UnityEngine.EventSystems;
using UnityEngine.Events;
using System;

public class Timer : MonoBehaviour {

	public float lastAmount;
	public float timerAmount;
	public float timeLeft;
	public bool Running;
	public bool TimerEnded;
	public InputField timerText;
	public Slider timerSlider;
	public Text buttonText;
	public AudioClip TimerEnd;
	public int hours;
	public int minutes;
	public int seconds;

	// Use this for initialization
	void Start (){
		Running = false;
		TimerEnded = true;
		timerText.text = "00:00:00";
	}
	public void StartPauseButtonClicked () {
		Running = !Running;
	}
	public void ResetButtonClicked () {
		TimerEnded = true;
		Running = false;
		timerText.text = "00:00:00";
	}
	// Update is called once per frame
	void Update () {
		if (TimerEnded == true) {
			timerText.interactable = true;
			buttonText.text = "Start";
			hours = int.Parse(timerText.text.Split (':') [0]);
			minutes = int.Parse(timerText.text.Split (':') [1]);
			seconds = int.Parse(timerText.text.Split (':') [2]);
			timerAmount = (3600 * float.Parse (timerText.text.Split (':') [0])) + (60 * float.Parse (timerText.text.Split (':') [1])) + (float.Parse (timerText.text.Split (':') [2]));
			timerSlider.maxValue = timerAmount;
			timeLeft = timerAmount;
			timerSlider.value = 0;
			lastAmount = timerAmount;
			if (Input.GetKeyDown (KeyCode.Return)) {
				Running = true;
			}
			if (Input.GetKeyDown (KeyCode.KeypadEnter)) {
				Running = true;
			}
		}
		if (Running == false) {
			buttonText.text = "Start";
		}
		if (Running == true) {
			timerText.interactable = false;
			buttonText.text = "Pause";
			TimerEnded = false;
			timeLeft -= Time.deltaTime;
			TimeSpan timespan = TimeSpan.FromSeconds(timeLeft);
			hours = timespan.Hours;
			minutes = timespan.Minutes;
			seconds = timespan.Seconds;
			timerSlider.value = timeLeft;
			if (hours > 0) {
				timerText.text = string.Format ("{0:0}:{1:0}:{2:00}", hours, minutes, seconds);
			}
			if (hours <= 0) {
				timerText.text = string.Format ("{0:0}:{1:00}", minutes, seconds);
			}
			if (minutes <= 0) {
				timerText.text = string.Format ("{0:00}", seconds);
			}
			if (timeLeft < 10) {
				timerText.text = string.Format ("{0:0}", seconds);
			}
			if (timeLeft <= 0) {
				AudioSource.PlayClipAtPoint(TimerEnd, new Vector3(0, 0, Camera.main.transform.position.z));
				TimeSpan previousAmount = TimeSpan.FromSeconds(lastAmount);
				hours = previousAmount.Hours;
				minutes = previousAmount.Minutes;
				seconds = previousAmount.Seconds;
				timerText.text = string.Format ("{0:00}:{1:00}:{2:00}", hours, minutes, seconds);
				TimerEnded = true;
				Running = false;
			}
		}
	}
}