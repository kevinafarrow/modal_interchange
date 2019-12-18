#!/usr/bin/env python3

scale_intervals=[2,2,1,2,2,2,1]
modes_starts=['ionian','dorian','phrygian','lydian','mixolydian','aeolian','locrean']
basic_notes=['C','D','E','F','G','A','B']
note_nums=['C','C#/Db','D','D#/Eb','E','F','F#/Gb','G','G#/Ab','A','A#/Bb','B']
possible_notes=[
    # 0
    ['B#', 'C' , 'Dbb' ],
    # 1
    ['BX', 'C#', 'Db' ],
    # 2
    ['CX', 'D' , 'Ebb' ],
    # 3
    ['D#', 'Eb' , 'Fbb' ],
    # 4
    ['DX', 'E' , 'Fb' ],
    # 5
    ['E#', 'F' , 'Gbb' ],
    # 6
    ['EX', 'F#', 'Gb' ],
    # 7
    ['FX', 'G' , 'Abb' ],
    # 8
    ['G#', 'Ab' ],
    # 9
    ['GX', 'A' , 'Bbb' ],
    # 10
    ['A#', 'Bb' , 'Cbb' ],
    # 11
    ['AX', 'B' , 'Cb' ]]

chord_values={
    '434' : 'Maj7' ,
    '433' : '7' ,
    '343' : '-7',
    '334' : '-7b5',
    '333' : 'dim7' ,
    '444' : 'aug7' }

def introduction():
    print('{:^24s}'.format("modal_interchange.py"))
    print('')
    print('A program to show the chords in parallell modes.')
    print('Enter a note and mode separated by a space and it will show you the')
    print('chords in the parallel modes.')
    print('Valid notes are:')
    print('  C, C#, Db, D, D#, Eb, E, F, F#, Gb, G, G#, Ab, A, A#, Bb, B')
    print('Valid scales are:')
    print('  ionian, major, dorian, phrygian, lydian, mixolydian, aeolian,')
    print('  minor, and locrean')
    print('')

def note_to_num(note):
    if len(note) == 1:
        note_num=note_nums.index(note)
    else:
        note_num=note_nums.index(note[0])
        for a in note[1:]:
            if a == '#':
                note_num=note_num+1
            if a == 'b' :
                note_num=note_num-1
    return note_num

def num_to_note(basic_note, num):
    basic_num=note_to_num(basic_note)
    x=basic_num-num
    if x == 0:
        correct_note=basic_note
    elif x > 0:
        correct_note=basic_note+(abs(x)*'b')
    elif x < 0:
        correct_note=basic_note+(abs(x)*'#')
    else: print('Check num_to_note')
    return correct_note

def scale_to_nums(scale):
    scale_nums=[]
    for n in scale:
        scale_nums.append(note_to_num(n))
    return scale_nums

def make_basic_scale(note):
    note_num=basic_notes.index(note[0])
    basic_scale=[]
    i=0
    while i < 7:
        basic_scale.append(basic_notes[note_num%7])
        note_num+=1
        i+=1
    return basic_scale

def make_scale_nums(note, mode):
    note_num=note_to_num(note)
    scale_nums=[]
    interval=modes_starts.index(mode)
    i=0
    while i < 7:
        scale_nums.append(note_num)
        note_num=(note_num+scale_intervals[interval%7])%12
        interval+=1
        i+=1
    return scale_nums

def make_scale(note, mode):
    # Make the basic scale
    basic_scale=make_basic_scale(note)
    # Make the correct numbers
    scale_nums=make_scale_nums(note, mode)
    # Make the correct notes
    correct_scale=[]
    i=0
    while i < 7:
        note_options=possible_notes[scale_nums[i]]
        for option in note_options:
            if option[0] == basic_scale[i]:
                correct_note=option
            else: pass
        correct_scale.append(correct_note)
        i+=1
    return correct_scale

def make_chord(note, scale):
    chord_notes=[]
    i=0
    while i < 4:
        chord_notes.append(note)
        note=scale[(scale.index(note)+2)%7]
        i+=1
    return chord_notes

def define_chord_type(chord_notes):
    chord_nums=[]
    minimum_num=note_to_num(chord_notes[0])
    for chord_note in chord_notes:
        chord_note_num=note_to_num(chord_note)
        if chord_note_num < minimum_num:
            chord_note_num=chord_note_num+12
        elif chord_note_num >= minimum_num:
            pass
        else: print("Check define_chord_type.")
        chord_nums.append(chord_note_num)
    intervalic_content=[]
    i=0
    while i < len(chord_nums)-1:
        interval=chord_nums[i+1]-chord_nums[i]
        intervalic_content.append(interval)
        i+=1
    chord_key=''
    for i in intervalic_content:
        chord_key=chord_key+str(i)
    chord_value=chord_values[chord_key]
    return chord_value

def make_scale_chords(scale):
    scale_chords=[]
    for scale_note in scale:
        scale_chord_notes=make_chord(scale_note, scale)
        scale_chord_value=define_chord_type(scale_chord_notes)
        scale_chord=scale_note+scale_chord_value
        scale_chords.append(scale_chord)
    return scale_chords

def string_to_print(array):
    string=''
    for x in array:
        string=string+x.ljust(10)
    return string

def main():
    introduction()
    while True:
        user_input=input('Please enter a note and mode separated by a space: ')
        user_input=user_input.split()
        note=user_input[0]
        mode=user_input[1]
        if mode == 'major' :
            mode='ionian'
        elif mode == 'minor' :
            mode='aeolian'
        else: pass
        # If you want to print the notes in the selected scale:
        # print('The notes in the ', note, mode, ' scale are:')
        # print(string_to_print(make_scale(note,mode)))
        print('')
        # If you want to see the notes in the parallel modes, uncomment here
        # ... or, you know, look at the notes of the chords below...
        # print('The parallel modes are as follows:')
        # for x in modes_starts:
        #     final=string_to_print(make_scale(note, x))
        #     print(note, x, '\t', final)
        # print('')
        print('The chords for all parallel modes are as follows:')
        print('')
        for x in modes_starts:
            chords=string_to_print(make_scale_chords(make_scale(note, x)))
            print(note, x, '\t', chords)
            print('')

main()
